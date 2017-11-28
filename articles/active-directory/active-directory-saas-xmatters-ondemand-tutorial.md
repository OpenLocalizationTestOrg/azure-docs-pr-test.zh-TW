---
title: "教學課程：Azure Active Directory 與 xMatters OnDemand 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 xMatters OnDemand 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="1dc47-103">教學課程：Azure Active Directory 與 xMatters OnDemand 整合</span><span class="sxs-lookup"><span data-stu-id="1dc47-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="1dc47-104">在此教學課程中，您學會如何 toointegrate xMatters OnDemand 的 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1dc47-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1dc47-105">整合 Azure AD 與 xMatters OnDemand 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1dc47-106">您可以控制存取 tooxMatters OnDemand 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1dc47-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="1dc47-107">您可以啟用您的使用者 tooautomatically get 登入 tooxMatters OnDemand （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1dc47-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1dc47-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1dc47-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1dc47-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc47-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dc47-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1dc47-110">Prerequisites</span></span>

<span data-ttu-id="1dc47-111">tooconfigure Azure AD 與 xMatters OnDemand 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="1dc47-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1dc47-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1dc47-113">已啟用 xMatters OnDemand 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1dc47-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1dc47-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1dc47-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1dc47-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1dc47-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1dc47-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1dc47-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1dc47-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1dc47-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1dc47-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1dc47-118">Scenario description</span></span>
<span data-ttu-id="1dc47-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1dc47-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1dc47-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1dc47-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1dc47-121">從 hello 圖庫加入 xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="1dc47-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="1dc47-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1dc47-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="1dc47-123">從 hello 圖庫加入 xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="1dc47-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="1dc47-124">tooconfigure hello 整合 xMatters OnDemand 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd xMatters OnDemand。</span><span class="sxs-lookup"><span data-stu-id="1dc47-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1dc47-125">**tooadd xMatters OnDemand 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1dc47-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc47-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1dc47-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1dc47-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1dc47-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1dc47-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1dc47-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1dc47-133">在 [hello] 搜尋方塊中，輸入**xMatters OnDemand**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="1dc47-135">在 hello 結果 窗格中，選取  **xMatters OnDemand**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1dc47-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1dc47-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1dc47-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1dc47-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 xMatters OnDemand 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1dc47-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1dc47-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello xMatters OnDemand 中的對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1dc47-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="1dc47-140">也就是說，連結之間的關聯性的 Azure AD 使用者和 hello 相關的使用者在 xMatters OnDemand 需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1dc47-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="1dc47-141">在 xMatters OnDemand 中，將指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1dc47-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1dc47-142">tooconfigure 和測試 Azure AD 單一登入與 xMatters OnDemand，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1dc47-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1dc47-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1dc47-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1dc47-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1dc47-145">**[建立 xMatters OnDemand 測試使用者](#creating-a-xmatters-ondemand-test-user)** -toohave xMatters OnDemand 所連結的 toohello Azure AD 使用者表示法的許 Simon 的對應項目。</span><span class="sxs-lookup"><span data-stu-id="1dc47-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1dc47-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1dc47-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1dc47-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1dc47-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1dc47-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1dc47-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1dc47-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您的 xMatters OnDemand 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="1dc47-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="1dc47-150">**tooconfigure Azure AD 單一登入與 xMatters OnDemand 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1dc47-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc47-151">在 Azure 入口網站上 hello hello **xMatters OnDemand**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1dc47-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1dc47-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="1dc47-155">在 hello **xMatters OnDemand 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="1dc47-157">a.</span><span class="sxs-lookup"><span data-stu-id="1dc47-157">a.</span></span> <span data-ttu-id="1dc47-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="1dc47-159">b.</span><span class="sxs-lookup"><span data-stu-id="1dc47-159">b.</span></span> <span data-ttu-id="1dc47-160">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="1dc47-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1dc47-161">These values are not real.</span></span> <span data-ttu-id="1dc47-162">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="1dc47-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="1dc47-163">請連絡[xMatters OnDemand 支援團隊](https://www.xmatters.com/company/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="1dc47-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="1dc47-164">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後 hello 憑證檔案儲存在本機上做為**c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="1dc47-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="1dc47-166">您需要 tooforward hello 憑證 toohello [xMatters OnDemand 支援團隊](https://www.xmatters.com/company/contact-us/)。</span><span class="sxs-lookup"><span data-stu-id="1dc47-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="1dc47-167">hello 憑證必須 toobe hello xMatters 支援小組所上傳，您才可以完成 hello 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="1dc47-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="1dc47-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1dc47-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1dc47-170">在 hello **xMatters OnDemand 設定**區段中，按一下**設定 xMatters OnDemand** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="1dc47-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1dc47-171">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="1dc47-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="1dc47-173">在不同的網頁瀏覽器視窗中，以登入 tooyour XMatters OnDemand 公司網站的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="1dc47-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="1dc47-174">在 hello hello 上方的工具列中按一下**Admin**，然後按一下**公司詳細資料**hello hello 左側導覽列中。</span><span class="sxs-lookup"><span data-stu-id="1dc47-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="1dc47-175">![管理](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "管理")</span><span class="sxs-lookup"><span data-stu-id="1dc47-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="1dc47-176">在 hello **SAML 設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="1dc47-177">![SAML 組態](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML 組態")</span><span class="sxs-lookup"><span data-stu-id="1dc47-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="1dc47-178">a.</span><span class="sxs-lookup"><span data-stu-id="1dc47-178">a.</span></span> <span data-ttu-id="1dc47-179">選取 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="1dc47-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="1dc47-180">b.</span><span class="sxs-lookup"><span data-stu-id="1dc47-180">b.</span></span> <span data-ttu-id="1dc47-181">貼上**SAML 實體識別碼**，其中您從 hello Azure 入口網站複製到 hello**身分識別提供者識別碼**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1dc47-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="1dc47-182">c.</span><span class="sxs-lookup"><span data-stu-id="1dc47-182">c.</span></span> <span data-ttu-id="1dc47-183">貼上**SAML 單一登入服務 URL**，其中您從 hello Azure 入口網站複製到 hello**單一登入 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1dc47-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="1dc47-184">d.</span><span class="sxs-lookup"><span data-stu-id="1dc47-184">d.</span></span> <span data-ttu-id="1dc47-185">貼上**登出 URL**，其中您從 hello Azure 入口網站複製到 hello**單一登出 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1dc47-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="1dc47-186">e.</span><span class="sxs-lookup"><span data-stu-id="1dc47-186">e.</span></span> <span data-ttu-id="1dc47-187">在 hello 公司詳細資料頁面上，在 hello 頂端，按一下 **儲存變更**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="1dc47-188">![公司詳細資料](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "公司詳細資料")</span><span class="sxs-lookup"><span data-stu-id="1dc47-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="1dc47-189">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1dc47-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1dc47-190">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1dc47-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1dc47-191">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1dc47-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1dc47-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1dc47-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="1dc47-193">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1dc47-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1dc47-195">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1dc47-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc47-196">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1dc47-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1dc47-198">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1dc47-200">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="1dc47-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1dc47-202">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1dc47-204">a.</span><span class="sxs-lookup"><span data-stu-id="1dc47-204">a.</span></span> <span data-ttu-id="1dc47-205">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1dc47-206">b.</span><span class="sxs-lookup"><span data-stu-id="1dc47-206">b.</span></span> <span data-ttu-id="1dc47-207">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1dc47-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1dc47-208">c.</span><span class="sxs-lookup"><span data-stu-id="1dc47-208">c.</span></span> <span data-ttu-id="1dc47-209">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1dc47-210">d.</span><span class="sxs-lookup"><span data-stu-id="1dc47-210">d.</span></span> <span data-ttu-id="1dc47-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1dc47-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="1dc47-212">建立 xMatters OnDemand 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1dc47-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="1dc47-213">在訂單 tooenable Azure AD 使用者 toolog tooXMatters OnDemand 中，您必須是佈建到 XMatters OnDemand。</span><span class="sxs-lookup"><span data-stu-id="1dc47-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="1dc47-214">在 XMatters OnDemand 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="1dc47-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="1dc47-215">tooprovision 使用者帳戶，執行下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="1dc47-216">登入 tooyour **XMatters OnDemand**租用戶。</span><span class="sxs-lookup"><span data-stu-id="1dc47-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="1dc47-217">按一下**使用者** 索引標籤，然後按一下**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="1dc47-218">![使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="1dc47-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="1dc47-219">在 hello**將使用者新增**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1dc47-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="1dc47-220">![加入使用者](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "加入使用者")</span><span class="sxs-lookup"><span data-stu-id="1dc47-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="1dc47-221">a.</span><span class="sxs-lookup"><span data-stu-id="1dc47-221">a.</span></span> <span data-ttu-id="1dc47-222">選取 [使用中] 。</span><span class="sxs-lookup"><span data-stu-id="1dc47-222">Select **Active**.</span></span>

    <span data-ttu-id="1dc47-223">b.</span><span class="sxs-lookup"><span data-stu-id="1dc47-223">b.</span></span> <span data-ttu-id="1dc47-224">在 hello**使用者識別碼**文字方塊中，例如使用者類型 hello 使用者識別碼Brittasimon@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="1dc47-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="1dc47-225">c.</span><span class="sxs-lookup"><span data-stu-id="1dc47-225">c.</span></span> <span data-ttu-id="1dc47-226">在 hello**名字**文字方塊中，像許 hello 使用者第一個型別名稱。</span><span class="sxs-lookup"><span data-stu-id="1dc47-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="1dc47-227">d.</span><span class="sxs-lookup"><span data-stu-id="1dc47-227">d.</span></span> <span data-ttu-id="1dc47-228">在 hello**姓氏**文字方塊中，姓氏類似 Simon hello 使用者類型。</span><span class="sxs-lookup"><span data-stu-id="1dc47-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="1dc47-229">e.</span><span class="sxs-lookup"><span data-stu-id="1dc47-229">e.</span></span> <span data-ttu-id="1dc47-230">在 hello**網站**文字方塊中，輸入 hello 有效的站台的有效 azure 想 tooprovision AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1dc47-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="1dc47-231">f.</span><span class="sxs-lookup"><span data-stu-id="1dc47-231">f.</span></span> <span data-ttu-id="1dc47-232">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1dc47-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1dc47-233">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="1dc47-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1dc47-234">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooxMatters OnDemand。</span><span class="sxs-lookup"><span data-stu-id="1dc47-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![指派使用者][200] 

<span data-ttu-id="1dc47-236">**tooassign 許 Simon tooxMatters OnDemand 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1dc47-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="1dc47-237">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1dc47-239">在 [hello] 應用程式清單中，選取**xMatters OnDemand**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![設定單一登入](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="1dc47-241">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1dc47-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1dc47-243">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1dc47-243">Click **Add** button.</span></span> <span data-ttu-id="1dc47-244">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1dc47-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1dc47-246">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="1dc47-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1dc47-247">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1dc47-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1dc47-248">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1dc47-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1dc47-249">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1dc47-249">Testing single sign-on</span></span>

<span data-ttu-id="1dc47-250">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1dc47-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1dc47-251">當您按一下 hello xMatters OnDemand 磚 hello 存取面板中時，您應該取得 tooyour 自動登入 xMatters OnDemand 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1dc47-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="1dc47-252">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="1dc47-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1dc47-253">其他資源</span><span class="sxs-lookup"><span data-stu-id="1dc47-253">Additional resources</span></span>

* [<span data-ttu-id="1dc47-254">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dc47-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1dc47-255">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1dc47-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

