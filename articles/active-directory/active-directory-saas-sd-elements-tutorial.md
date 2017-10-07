---
title: "教學課程：Azure Active Directory 與 SD Elements 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SD 元素之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0386307-bb3b-4810-8d4b-d0bfebda04f4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 77949e41beb541c9fe8147b1eb2e7995e05bd753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sd-elements"></a><span data-ttu-id="9f9fe-103">教學課程：Azure Active Directory 與 SD Elements 整合</span><span class="sxs-lookup"><span data-stu-id="9f9fe-103">Tutorial: Azure Active Directory integration with SD Elements</span></span>

<span data-ttu-id="9f9fe-104">在此教學課程中，您學會如何 toointegrate SD 與 Azure Active Directory (Azure AD) 的項目。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-104">In this tutorial, you learn how toointegrate SD Elements with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f9fe-105">使用 Azure AD 整合 SD 項目可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-105">Integrating SD Elements with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f9fe-106">您可以控制在 Azure AD 中擁有存取 tooSD 項目</span><span class="sxs-lookup"><span data-stu-id="9f9fe-106">You can control in Azure AD who has access tooSD Elements</span></span>
- <span data-ttu-id="9f9fe-107">您可以啟用您的使用者 tooautomatically get 登入 tooSD （單一登入） 的項目與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="9f9fe-107">You can enable your users tooautomatically get signed-on tooSD Elements (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f9fe-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9f9fe-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f9fe-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f9fe-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9f9fe-110">Prerequisites</span></span>

<span data-ttu-id="9f9fe-111">tooconfigure SD 項目與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-111">tooconfigure Azure AD integration with SD Elements, you need hello following items:</span></span>

- <span data-ttu-id="9f9fe-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9f9fe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f9fe-113">已啟用 SD Elements 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="9f9fe-113">A SD Elements single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f9fe-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f9fe-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="9f9fe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f9fe-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f9fe-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f9fe-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9f9fe-118">Scenario description</span></span>
<span data-ttu-id="9f9fe-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f9fe-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9f9fe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f9fe-121">從 hello 組件庫加入 SD 元素</span><span class="sxs-lookup"><span data-stu-id="9f9fe-121">Adding SD Elements from hello gallery</span></span>
2. <span data-ttu-id="9f9fe-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9f9fe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sd-elements-from-hello-gallery"></a><span data-ttu-id="9f9fe-123">從 hello 組件庫加入 SD 元素</span><span class="sxs-lookup"><span data-stu-id="9f9fe-123">Adding SD Elements from hello gallery</span></span>
<span data-ttu-id="9f9fe-124">tooconfigure hello 整合 SD 項目到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SD 項目。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-124">tooconfigure hello integration of SD Elements into Azure AD, you need tooadd SD Elements from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f9fe-125">**tooadd hello 圖庫中，從 SD 項目執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f9fe-125">**tooadd SD Elements from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9fe-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9f9fe-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f9fe-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9f9fe-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9f9fe-133">在 [hello] 搜尋方塊中，輸入**SD 元素**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-133">In hello search box, type **SD Elements**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_search.png)

5. <span data-ttu-id="9f9fe-135">在 hello 結果 窗格中，選取  **SD 項目**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-135">In hello results panel, select **SD Elements**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f9fe-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9f9fe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f9fe-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 SD Elements 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-138">In this section, you configure and test Azure AD single sign-on with SD Elements based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9f9fe-139">單一登入 toowork，Azure AD 需要 tooknow SD 項目中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SD Elements is tooa user in Azure AD.</span></span> <span data-ttu-id="9f9fe-140">換句話說，Azure AD 使用者與 hello SD 項目中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-140">In other words, a link relationship between an Azure AD user and hello related user in SD Elements needs toobe established.</span></span>

<span data-ttu-id="9f9fe-141">SD 元素中指定的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-141">In SD Elements, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f9fe-142">tooconfigure 及測試 Azure AD 單一登入與 SD 項目，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-142">tooconfigure and test Azure AD single sign-on with SD Elements, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f9fe-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f9fe-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f9fe-145">**[建立 SD 元素測試使用者](#creating-a-sd-elements-test-user)** -toohave 許 Simon SD 元素是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-145">**[Creating a SD Elements test user](#creating-a-sd-elements-test-user)** - toohave a counterpart of Britta Simon in SD Elements that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f9fe-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f9fe-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f9fe-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9f9fe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f9fe-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 SD 項目在應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SD Elements application.</span></span>

<span data-ttu-id="9f9fe-150">**tooconfigure Azure AD 單一登入 SD 項目時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f9fe-150">**tooconfigure Azure AD single sign-on with SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9fe-151">在 Azure 入口網站上 hello hello **SD 元素**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-151">In hello Azure portal, on hello **SD Elements** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9f9fe-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_samlbase.png)

3. <span data-ttu-id="9f9fe-155">在 hello **SD 元素網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-155">On hello **SD Elements Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_url.png)

    <span data-ttu-id="9f9fe-157">a.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-157">a.</span></span> <span data-ttu-id="9f9fe-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.sdelements.com/sso/saml2/metadata`</span><span class="sxs-lookup"><span data-stu-id="9f9fe-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/metadata`</span></span>

    <span data-ttu-id="9f9fe-159">b.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-159">b.</span></span> <span data-ttu-id="9f9fe-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.sdelements.com/sso/saml2/acs/`</span><span class="sxs-lookup"><span data-stu-id="9f9fe-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<tenantname>.sdelements.com/sso/saml2/acs/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f9fe-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-161">These values are not real.</span></span> <span data-ttu-id="9f9fe-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9f9fe-163">請連絡[SD 項目支援小組](mailto:support@sdelements.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-163">Contact [SD Elements support team](mailto:support@sdelements.com) tooget these values.</span></span>

4. <span data-ttu-id="9f9fe-164">SD 項目的應用程式預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-164">SD Elements application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9f9fe-165">設定下列宣告為此應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="9f9fe-166">您可以從 hello 管理這些屬性的 hello 值**使用者屬性** hello 應用程式 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-166">You can manage hello values of these attributes from hello **"User Attribute"** tab of hello application.</span></span> <span data-ttu-id="9f9fe-167">hello 下列螢幕擷取畫面會顯示這個範例。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-167">hello following screenshot shows an example for this.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_attribute.png)

5. <span data-ttu-id="9f9fe-169">在 hello**使用者屬性**hello 區段**單一登入** 對話方塊中，hello 映像中所示設定 SAML 權杖屬性並執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-169">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span> 

    | <span data-ttu-id="9f9fe-170">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="9f9fe-170">Attribute Name</span></span> | <span data-ttu-id="9f9fe-171">屬性值</span><span class="sxs-lookup"><span data-stu-id="9f9fe-171">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9f9fe-172">電子郵件</span><span class="sxs-lookup"><span data-stu-id="9f9fe-172">email</span></span> |<span data-ttu-id="9f9fe-173">user.mail</span><span class="sxs-lookup"><span data-stu-id="9f9fe-173">user.mail</span></span> |
    | <span data-ttu-id="9f9fe-174">firstname</span><span class="sxs-lookup"><span data-stu-id="9f9fe-174">firstname</span></span> |<span data-ttu-id="9f9fe-175">user.givenname</span><span class="sxs-lookup"><span data-stu-id="9f9fe-175">user.givenname</span></span> |
    | <span data-ttu-id="9f9fe-176">lastname</span><span class="sxs-lookup"><span data-stu-id="9f9fe-176">lastname</span></span> |<span data-ttu-id="9f9fe-177">user.surname</span><span class="sxs-lookup"><span data-stu-id="9f9fe-177">user.surname</span></span> |

    <span data-ttu-id="9f9fe-178">a.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-178">a.</span></span> <span data-ttu-id="9f9fe-179">按一下**加入屬性**tooopen hello**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_04.png)

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="9f9fe-182">b.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-182">b.</span></span> <span data-ttu-id="9f9fe-183">在 hello**名稱**文字方塊中，該資料列所顯示的型別 hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="9f9fe-184">c.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-184">c.</span></span> <span data-ttu-id="9f9fe-185">從 hello**值**清單，顯示該資料列的型別 hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="9f9fe-186">d.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-186">d.</span></span> <span data-ttu-id="9f9fe-187">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-187">Click **Ok**.</span></span>
 
6. <span data-ttu-id="9f9fe-188">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_certificate.png) 

7. <span data-ttu-id="9f9fe-190">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-190">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9f9fe-192">在 hello **SD 項目組態**區段中，按一下**設定 SD 項目**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-192">On hello **SD Elements Configuration** section, click **Configure SD Elements** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9f9fe-193">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="9f9fe-193">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_configure.png)

9. <span data-ttu-id="9f9fe-195">tooget 單一登入啟用，請連絡您[SD 項目支援小組](mailto:support@sdelements.com)並提供他們最 hello 下載的憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-195">tooget single sign-on enabled, contact your [SD Elements support team](mailto:support@sdelements.com) and provide them with hello downloaded certificate file.</span></span> 

10. <span data-ttu-id="9f9fe-196">在不同的瀏覽器視窗中，以系統管理員身分登入 tooyour SD 元素租用戶。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-196">In a different browser window, sign-on tooyour SD Elements tenant as an administrator.</span></span>

11. <span data-ttu-id="9f9fe-197">在 hello 最上層顯示 hello 功能表上，按一下**系統**，然後**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-197">In hello menu on hello top, click **System**, and then **Single Sign-on**.</span></span> 
   
    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_09.png) 

12. <span data-ttu-id="9f9fe-199">在 [hello**單一登入設定**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-199">On hello **Single Sign-On Settings** dialog, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_10.png) 
   
    <span data-ttu-id="9f9fe-201">a.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-201">a.</span></span> <span data-ttu-id="9f9fe-202">[SSO 類型] 請選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-202">As **SSO Type**, select **SAML**.</span></span>
   
    <span data-ttu-id="9f9fe-203">b.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-203">b.</span></span> <span data-ttu-id="9f9fe-204">在 hello**身分識別提供者的實體識別碼**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-204">In hello **Identity Provider Entity ID** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="9f9fe-205">c.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-205">c.</span></span> <span data-ttu-id="9f9fe-206">在 hello**身分識別提供者單一登入服務**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-206">In hello **Identity Provider Single Sign-On Service** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span> 
   
    <span data-ttu-id="9f9fe-207">d.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-207">d.</span></span> <span data-ttu-id="9f9fe-208">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-208">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9f9fe-209">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="9f9fe-209">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f9fe-210">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-210">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f9fe-211">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f9fe-211">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f9fe-212">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9f9fe-212">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f9fe-213">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-213">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9f9fe-215">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f9fe-215">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9fe-216">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-216">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f9fe-218">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-218">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f9fe-220">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-220">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f9fe-222">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-222">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sd-elements-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f9fe-224">a.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-224">a.</span></span> <span data-ttu-id="9f9fe-225">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-225">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f9fe-226">b.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-226">b.</span></span> <span data-ttu-id="9f9fe-227">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-227">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f9fe-228">c.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-228">c.</span></span> <span data-ttu-id="9f9fe-229">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-229">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f9fe-230">d.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-230">d.</span></span> <span data-ttu-id="9f9fe-231">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-231">Click **Create**.</span></span>
 
### <a name="creating-a-sd-elements-test-user"></a><span data-ttu-id="9f9fe-232">建立 SD Elements 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9f9fe-232">Creating a SD Elements test user</span></span>

<span data-ttu-id="9f9fe-233">hello 本節目標在於 toocreate 呼叫許 Simon SD 項目中的使用者。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-233">hello objective of this section is toocreate a user called Britta Simon in SD Elements.</span></span> <span data-ttu-id="9f9fe-234">SD 元素的 hello 案例中，建立 SD 項目的使用者，是一項手動工作。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-234">In hello case of SD Elements, creating SD Elements users is a manual task.</span></span>

<span data-ttu-id="9f9fe-235">**toocreate 許 Simon SD 元素中執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f9fe-235">**toocreate Britta Simon in SD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9fe-236">在 web 瀏覽器視窗中，以系統管理員身分登入 tooyour SD 元素公司網站。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-236">In a web browser window, sign-on tooyour SD Elements company site as an administrator.</span></span>

2. <span data-ttu-id="9f9fe-237">在 hello 最上層顯示 hello 功能表上，按一下**使用者管理**，然後**使用者**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-237">In hello menu on hello top, click **User Management**, and then **Users**.</span></span>
   
    ![建立 SD Elements 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_11.png) 

3. <span data-ttu-id="9f9fe-239">按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-239">Click **Add New User**.</span></span>
   
    ![建立 SD Elements 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_12.png)
 
4. <span data-ttu-id="9f9fe-241">在 [hello**新增使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9f9fe-241">On hello **Add New User** dialog, perform hello following steps:</span></span>
   
    ![建立 SD Elements 測試使用者](./media/active-directory-saas-sd-elements-tutorial/tutorial_sd-elements_13.png) 
   
    <span data-ttu-id="9f9fe-243">a.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-243">a.</span></span> <span data-ttu-id="9f9fe-244">在 hello**電子郵件**文字方塊中，輸入 hello 電子郵件的使用者，例如 **brittasimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-244">In hello **E-mail** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
    <span data-ttu-id="9f9fe-245">b.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-245">b.</span></span> <span data-ttu-id="9f9fe-246">在 hello**名字**文字方塊中，輸入 hello 名字，例如使用者的**許**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-246">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>
   
    <span data-ttu-id="9f9fe-247">c.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-247">c.</span></span> <span data-ttu-id="9f9fe-248">在 hello**姓氏**文字方塊中，輸入 hello 姓氏的使用者，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-248">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>
   
    <span data-ttu-id="9f9fe-249">d.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-249">d.</span></span> <span data-ttu-id="9f9fe-250">針對 [角色]，選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-250">As **Role**, select **User**.</span></span> 
   
    <span data-ttu-id="9f9fe-251">e.</span><span class="sxs-lookup"><span data-stu-id="9f9fe-251">e.</span></span> <span data-ttu-id="9f9fe-252">按一下 [建立使用者] 。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-252">Click **Create User**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f9fe-253">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="9f9fe-253">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f9fe-254">本節中，在您啟用 Azure 單一登入許 Simon toouse tooSD 項目授與存取權。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-254">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSD Elements.</span></span>

![指派使用者][200] 

<span data-ttu-id="9f9fe-256">**tooassign 許 Simon tooSD 項目，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9f9fe-256">**tooassign Britta Simon tooSD Elements, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f9fe-257">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-257">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9f9fe-259">在 [hello] 應用程式清單中，選取**SD 元素**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-259">In hello applications list, select **SD Elements**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sd-elements-tutorial/tutorial_sdelements_app.png) 

3. <span data-ttu-id="9f9fe-261">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-261">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9f9fe-263">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-263">Click **Add** button.</span></span> <span data-ttu-id="9f9fe-264">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-264">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9f9fe-266">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-266">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f9fe-267">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-267">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f9fe-268">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-268">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f9fe-269">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9f9fe-269">Testing single sign-on</span></span>

<span data-ttu-id="9f9fe-270">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-270">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>
  
<span data-ttu-id="9f9fe-271">當您按一下的 hello SD 項目磚 hello 存取面板中時，您應該取得自動登入 tooyour SD 項目的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f9fe-271">When you click hello SD Elements tile in hello Access Panel, you should get automatically signed-on tooyour SD Elements application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f9fe-272">其他資源</span><span class="sxs-lookup"><span data-stu-id="9f9fe-272">Additional resources</span></span>

* [<span data-ttu-id="9f9fe-273">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f9fe-273">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f9fe-274">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9f9fe-274">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sd-elements-tutorial/tutorial_general_203.png

