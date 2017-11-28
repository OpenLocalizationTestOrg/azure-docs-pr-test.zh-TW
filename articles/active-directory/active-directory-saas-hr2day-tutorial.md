---
title: "教學課程：Azure Active Directory 與 HR2day by Merces 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與由 Merces HR2day 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="9ce7a-103">教學課程：Azure Active Directory 與 HR2day by Merces 整合</span><span class="sxs-lookup"><span data-stu-id="9ce7a-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="9ce7a-104">在此教學課程中，您學會如何 toointegrate HR2day 由 Merces 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-104">In this tutorial, you learn how toointegrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9ce7a-105">與 Azure AD 整合所 Merces HR2day 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="9ce7a-105">Integrating HR2day by Merces with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9ce7a-106">您可以控制存取 tooHR2day Merces 由 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-106">You can control in Azure AD who has access tooHR2day by Merces.</span></span>
- <span data-ttu-id="9ce7a-107">您可以啟用 tooautomatically 取得登入 tooHR2day Merces 其 Azure AD 帳戶與您的使用者。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-107">You can enable your users tooautomatically get signed in tooHR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="9ce7a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-108">You can manage your accounts in one central location--hello Azure portal.</span></span>

<span data-ttu-id="9ce7a-109">如需 SaaS 應用程式與 Azure AD 整合的詳細資訊，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ce7a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="9ce7a-110">Prerequisites</span></span>

<span data-ttu-id="9ce7a-111">tooconfigure HR2day Merces 所使用的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="9ce7a-111">tooconfigure Azure AD integration with HR2day by Merces, you need hello following items:</span></span>

- <span data-ttu-id="9ce7a-112">Azure AD 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="9ce7a-113">已啟用 HR2day by Merces 單一登入的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="9ce7a-114">我們不建議使用實際執行環境 tootest hello 本教學課程中的步驟。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-114">We don't recommend using a production environment tootest hello steps in this tutorial.</span></span>

<span data-ttu-id="9ce7a-115">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="9ce7a-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="9ce7a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="9ce7a-117">如果您沒有 Azure AD，可取得 [Azure AD 一個月免費試用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="9ce7a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="9ce7a-118">Scenario description</span></span>
<span data-ttu-id="9ce7a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9ce7a-120">此處概述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="9ce7a-120">hello scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="9ce7a-121">新增由 Merces HR2day 從 hello 組件庫。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-121">Adding HR2day by Merces from hello gallery.</span></span>
2. <span data-ttu-id="9ce7a-122">設定並測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-hello-gallery"></a><span data-ttu-id="9ce7a-123">從 hello 圖庫新增由 Merces HR2day</span><span class="sxs-lookup"><span data-stu-id="9ce7a-123">Add HR2day by Merces from hello gallery</span></span>
<span data-ttu-id="9ce7a-124">tooconfigure hello 整合由 Merces HR2day 到 Azure AD 中，加入所 Merces HR2day hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-124">tooconfigure hello integration of HR2day by Merces into Azure AD, add HR2day by Merces from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9ce7a-125">**tooadd HR2day Merces hello 圖庫中，從所採取下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9ce7a-125">**tooadd HR2day by Merces from hello gallery, take hello following steps:**</span></span>

1. <span data-ttu-id="9ce7a-126">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左側的導覽窗格中，選取 hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-126">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9ce7a-128">跳過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-128">Go too**Enterprise applications**.</span></span> <span data-ttu-id="9ce7a-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="9ce7a-131">tooadd 新的應用程式中，選取 hello**新的應用程式**hello 頂端 hello 對話方塊上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-131">tooadd a new application, select hello **New application** button on hello top of hello dialog box.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="9ce7a-133">在 [hello] 搜尋方塊中，輸入**由 Merces HR2day**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-133">In hello search box, type **HR2day by Merces**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="9ce7a-135">在 hello 結果 窗格中，選取**由 Merces HR2day**，然後選取 hello**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-135">In hello results panel, select **HR2day by Merces**, and then select hello **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9ce7a-137">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9ce7a-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="9ce7a-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 HR2day by Merces 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9ce7a-139">Azure AD 單一登入 toowork，需要 tooknow 負責 hello 對等項目的使用者中由 Merces HR2day tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-139">For single sign-on toowork, Azure AD needs tooknow who hello counterpart user in HR2day by Merces is tooa user in Azure AD.</span></span> <span data-ttu-id="9ce7a-140">換句話說，您需要 tooestablish Azure AD 使用者與 hello 由 Merces HR2day 中相關的使用者之間的連結。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-140">In other words, you need tooestablish a link between an Azure AD user and hello related user in HR2day by Merces.</span></span>

<span data-ttu-id="9ce7a-141">在由 Merces HR2day，將指派 hello**使用者名稱**在 Azure AD 中太**Username** tooestablish hello 關聯性。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-141">In HR2day by Merces, assign hello **user name** in Azure AD too **Username** tooestablish hello relationship.</span></span>

<span data-ttu-id="9ce7a-142">tooconfigure 及測試 HR2day Merces 由 Azure AD 單一登入，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="9ce7a-142">tooconfigure and test Azure AD single sign-on with HR2day by Merces, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9ce7a-143">[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)： 啟用使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users toouse this feature.</span></span>
2. <span data-ttu-id="9ce7a-144">[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)：使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9ce7a-145">[建立由 Merces 測試使用者 HR2day](#creating-an-hr2day-by-merces-test-user)： 在由是連結的 toohello Azure AD 使用者表示法的 Merces HR2day 建立許 Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9ce7a-146">[指派給 Azure AD hello 測試使用者](#assigning-the-azure-ad-test-user)： 啟用許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-146">[Assign hello Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9ce7a-147">[測試單一登入](#testing-single-sign-on)： 驗證是否 hello 設定可正常運作。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-147">[Test single sign-on](#testing-single-sign-on): Verify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9ce7a-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="9ce7a-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9ce7a-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入在您 HR2day Merces 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="9ce7a-150">**tooconfigure Azure AD 單一登入與 HR2day 由 Merces，採取下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9ce7a-150">**tooconfigure Azure AD single sign-on with HR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="9ce7a-151">在 Azure 入口網站上 hello hello**由 Merces HR2day**應用程式整合頁面上，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-151">In hello Azure portal, on hello **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="9ce7a-153">tooenable 單一登入，在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-153">tooenable single sign-on, in hello **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="9ce7a-155">在 hello **Merces 網域和 Url HR2day**區段中，採取下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="9ce7a-155">In hello **HR2day by Merces Domain and URLs** section, take hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="9ce7a-157">a.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-157">a.</span></span> <span data-ttu-id="9ce7a-158">在 hello**登入 URL**方塊中，輸入 URL，使用下列模式的 hello: `https://<tenantname>.force.com/<instancename>`。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-158">In hello **Sign-on URL** box, type a URL by using hello following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="9ce7a-159">b.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-159">b.</span></span> <span data-ttu-id="9ce7a-160">在 hello**識別碼**方塊中，輸入 URL，使用下列模式的 hello: `https://hr2day.force.com/<companyname>`。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-160">In hello **Identifier** box, type a URL by using hello following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9ce7a-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-161">These values are not real.</span></span> <span data-ttu-id="9ce7a-162">更新這些值與 hello 實際登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-162">Update these values with hello actual sign-on URL and identifier.</span></span> <span data-ttu-id="9ce7a-163">連絡 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl) tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-163">Contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl) tooget these values.</span></span> 
 


4. <span data-ttu-id="9ce7a-164">在 hello **SAML 簽章憑證**區段中，選取**Certificate(Base64)**，然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-164">On hello **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="9ce7a-166">本章節描述如何 tooenable 使用者 tooauthenticate tooHR2day 由 Merces 與 Azure AD 的帳戶。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-166">This section describes how tooenable users tooauthenticate tooHR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="9ce7a-167">他們這麼做，使用 hello SAML 通訊協定為基礎的同盟。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-167">They do this by using federation that's based on hello SAML protocol.</span></span>

    <span data-ttu-id="9ce7a-168">您 HR2day Merces 應用程式所預期 hello SAML 判斷提示，以特定格式，這需要您 tooadd 自訂屬性對應 tooyour SAML 權杖。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-168">Your HR2day by Merces application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token.</span></span> <span data-ttu-id="9ce7a-169">hello 下列螢幕擷取畫面顯示此動作的範例。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-169">hello following screenshot shows an example of this.</span></span> 

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="9ce7a-171">您可以設定 hello SAML 判斷提示之前，您必須連絡 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl)並要求您的租用戶 hello hello 唯一識別碼屬性值。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-171">Before you can configure hello SAML assertion, you must contact hello [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="9ce7a-172">您需要此值 toocomplete hello 中的步驟 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-172">You need this value toocomplete hello steps in hello next section.</span></span> 

6. <span data-ttu-id="9ce7a-173">在 hello**單一登入**對話方塊中的，在 hello**使用者屬性**區段中，設定 hello SAML 權杖屬性 hello 下列影像所示。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-173">In hello **Single sign-on** dialog box, in hello **User Attributes** section, configure hello SAML token attribute as shown in hello following image.</span></span> <span data-ttu-id="9ce7a-174">接著採取下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-174">Then take hello following steps.</span></span>
    
      | <span data-ttu-id="9ce7a-175">屬性名稱</span><span class="sxs-lookup"><span data-stu-id="9ce7a-175">Attribute name</span></span>    |   <span data-ttu-id="9ce7a-176">屬性值</span><span class="sxs-lookup"><span data-stu-id="9ce7a-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="9ce7a-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="9ce7a-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="9ce7a-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="9ce7a-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="9ce7a-179">a.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-179">a.</span></span> <span data-ttu-id="9ce7a-180">tooopen hello**加入屬性**對話方塊中，選取**加入屬性**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-180">tooopen hello **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="9ce7a-183">b.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-183">b.</span></span> <span data-ttu-id="9ce7a-184">在 hello**名稱**方塊中，輸入**ATTR_LOGINCLAIM**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-184">In hello **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="9ce7a-185">c.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-185">c.</span></span> <span data-ttu-id="9ce7a-186">從 hello**值**清單中，選取**join （)**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-186">From hello **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="9ce7a-187">d.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-187">d.</span></span> <span data-ttu-id="9ce7a-188">從 hello **String1**清單中，選取**user.mail**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-188">From hello **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="9ce7a-189">e.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-189">e.</span></span> <span data-ttu-id="9ce7a-190">如**String2**，輸入 hello HR2day 小組所提供的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-190">For **String2**, type hello unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="9ce7a-191">f.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-191">f.</span></span> <span data-ttu-id="9ce7a-192">在 hello**分隔符號**方塊中，輸入 **@** 。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-192">In hello **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="9ce7a-193">g.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-193">g.</span></span> <span data-ttu-id="9ce7a-194">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-194">Select **Ok**.</span></span>

7. <span data-ttu-id="9ce7a-195">選取 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-195">Select hello **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9ce7a-197">在 hello **HR2day Merces 組態**區段中，選取**設定 HR2day Merces 所**tooopen hello**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-197">In hello **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** tooopen hello **Configure sign-on** window.</span></span> <span data-ttu-id="9ce7a-198">複製 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**從 hello**快速參考**> 一節。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-198">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference** section.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="9ce7a-200">您的應用程式，請連絡 hello tooconfigure SSO [Merces 用戶端支援小組 HR2day](mailTo:servicedesk@merces.nl)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-200">tooconfigure SSO  for your application, contact hello [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="9ce7a-201">附加 hello 下載**Certificate(Base64)**檔案 tooyour 電子郵件。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-201">Attach hello downloaded **Certificate(Base64)** file tooyour email.</span></span> <span data-ttu-id="9ce7a-202">也提供 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL** ，讓它們可以設定為 SSO 整合。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-202">Also provide hello **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="9ce7a-203">提到 toohello Merces 小組的這項整合需要 hello 與 hello 模式設定的實體識別碼 toobe **https://hr2day.force.com/INSTANCENAME**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-203">Mention toohello Merces team that this integration needs hello Entity ID toobe set with hello pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="9ce7a-204">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="9ce7a-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9ce7a-205">將此應用程式從 hello 後**Active Directory** > **企業應用程式**區段中，選取 hello**單一登入** 索引標籤。然後存取 hello 內嵌文件，透過 hello**組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-205">After you add this app from hello **Active Directory** > **Enterprise Applications** section, select hello **Single Sign-On** tab. Then access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9ce7a-206">閱讀更多有關 hello embedded 文件功能的 hello [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-206">You can read more about hello embedded documentation feature in hello [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9ce7a-207">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9ce7a-207">Create an Azure AD test user</span></span>
<span data-ttu-id="9ce7a-208">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="9ce7a-210">**toocreate 在 Azure AD 中的測試使用者採取下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9ce7a-210">**toocreate a test user in Azure AD, take hello following steps:**</span></span>

1. <span data-ttu-id="9ce7a-211">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，選取 hello **Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-211">In hello **Azure portal**, on hello left navigation pane, select hello **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9ce7a-213">toodisplay hello 使用者清單，請移過**使用者和群組**，然後選取**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-213">toodisplay hello list of users, go too**Users and groups**, and then select **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9ce7a-215">tooopen hello**使用者**對話方塊中，選取**新增**hello 最上層顯示 hello 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-215">tooopen hello **User** dialog box, select **Add** on hello top of hello dialog box.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9ce7a-217">在 hello**使用者**對話方塊中，接受 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9ce7a-217">In hello **User** dialog box, take hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9ce7a-219">a.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-219">a.</span></span> <span data-ttu-id="9ce7a-220">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-220">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9ce7a-221">b.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-221">b.</span></span> <span data-ttu-id="9ce7a-222">在 [hello**使用者名**] 方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-222">In hello **User name** box, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9ce7a-223">c.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-223">c.</span></span> <span data-ttu-id="9ce7a-224">選取**顯示密碼**，然後記下 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-224">Select **Show Password**, and then write down hello password.</span></span>

    <span data-ttu-id="9ce7a-225">d.</span><span class="sxs-lookup"><span data-stu-id="9ce7a-225">d.</span></span> <span data-ttu-id="9ce7a-226">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-226">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="9ce7a-227">建立 HR2day by Merces 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9ce7a-227">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="9ce7a-228">hello 本節目標在於 toocreate HR2day 中呼叫 Merces 許 Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-228">hello objective of this section is toocreate a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="9ce7a-229">在 hello HR2day 帳戶 tooadd hello 使用者處理 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-229">tooadd hello users in hello HR2day account, work with hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="9ce7a-230">若要手動 toocreate 使用者，請連絡 hello [Merces 用戶端支援小組 HR2day](mailto:servicedesk@merces.nl)。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-230">If you need toocreate a user manually, contact hello [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9ce7a-231">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="9ce7a-231">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9ce7a-232">在本節中，您可以授與由 Merces 她存取 tooHR2day 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooHR2day by Merces.</span></span>

![指派使用者][200] 

<span data-ttu-id="9ce7a-234">**tooassign 許 Simon tooHR2day 由 Merces，採取下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="9ce7a-234">**tooassign Britta Simon tooHR2day by Merces, take hello following steps:**</span></span>

1. <span data-ttu-id="9ce7a-235">在 hello Azure 入口網站，開啟 hello 應用程式檢視、 移 toohello 目錄檢視，並前往太**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-235">In hello Azure portal, open hello applications view, go toohello directory view, and then go too**Enterprise applications**.</span></span> <span data-ttu-id="9ce7a-236">接著，選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-236">Next, select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="9ce7a-238">在 [hello] 應用程式清單中，選取**由 Merces HR2day**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-238">In hello applications list, select **HR2day by Merces**.</span></span>

    ![設定單一登入](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="9ce7a-240">在左側 hello hello 功能表中選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-240">In hello menu on hello left, select **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="9ce7a-242">選取 hello**新增** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-242">Select hello **Add** button.</span></span> <span data-ttu-id="9ce7a-243">然後，在 hello**將作業加入**對話方塊中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-243">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="9ce7a-245">在 hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-245">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="9ce7a-246">按一下 hello**選取** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-246">Click hello **Select** button.</span></span>

7. <span data-ttu-id="9ce7a-247">在 hello**將作業加入**對話方塊中，選取**指派**。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-247">In hello **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9ce7a-248">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="9ce7a-248">Test single sign-on</span></span>

<span data-ttu-id="9ce7a-249">hello 本節的目標是 tootest 您 Azure AD 單一登入的組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-249">hello objective of this section is tootest your Azure AD single sign-on configuration by using hello Access Panel.</span></span>  

<span data-ttu-id="9ce7a-250">當您選取 hello HR2day 由 Merces 磚 hello 存取面板中時，您會自動取得登入 tooyour HR2day Merces 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ce7a-250">When you select hello HR2day by Merces tile in hello Access Panel, you automatically get signed in  tooyour HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9ce7a-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="9ce7a-251">Additional resources</span></span>

* [<span data-ttu-id="9ce7a-252">教學課程有關清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ce7a-252">List of tutorials about how tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9ce7a-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="9ce7a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

