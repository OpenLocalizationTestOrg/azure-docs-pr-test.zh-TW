---
title: "教學課程：Azure Active Directory 與 IBM Kenexa Survey Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 IBM Kenexa 調查企業之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="ae20a-103">教學課程：Azure Active Directory 與 IBM Kenexa Survey Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="ae20a-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="ae20a-104">在此教學課程中，您學會如何 toointegrate IBM Kenexa 調查企業與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-104">In this tutorial, you learn how toointegrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae20a-105">與 Azure AD 整合 IBM Kenexa 調查 Enterprise 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ae20a-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ae20a-106">您可以控制存取 tooIBM Kenexa 調查 Enterprise 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ae20a-106">You can control in Azure AD who has access tooIBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="ae20a-107">您可以啟用您的使用者 tooautomatically 登入 tooIBM Kenexa 調查企業單一登入 (SSO) 使用其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae20a-107">You can enable your users tooautomatically sign in tooIBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="ae20a-108">您可以管理您的帳戶，在單一中央位置： hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ae20a-108">You can manage your accounts in one central location: hello Azure portal.</span></span>

<span data-ttu-id="ae20a-109">如果您想 tooknow 更多關於軟體使用 Azure AD 服務 (SaaS) 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-109">If you want tooknow more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae20a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ae20a-110">Prerequisites</span></span>

<span data-ttu-id="ae20a-111">tooconfigure 與 IBM Kenexa 調查 Enterprise 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ae20a-111">tooconfigure Azure AD integration with IBM Kenexa Survey Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="ae20a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ae20a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae20a-113">啟用 IBM Kenexa Survey Enterprise SSO 的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ae20a-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae20a-114">當您測試 hello 步驟在本教學課程時，我們建議您不要使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ae20a-114">When you test hello steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="ae20a-115">tootest hello 步驟在本教學課程，請遵循下列建議：</span><span class="sxs-lookup"><span data-stu-id="ae20a-115">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ae20a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ae20a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae20a-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae20a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ae20a-118">Scenario description</span></span>
<span data-ttu-id="ae20a-119">在本教學課程中，您會在測試環境中測試 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="ae20a-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="ae20a-120">hello hello 教學課程所述的案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ae20a-120">hello scenario outlined in hello tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="ae20a-121">從 hello 圖庫加入 IBM Kenexa 調查 Enterprise</span><span class="sxs-lookup"><span data-stu-id="ae20a-121">Adding IBM Kenexa Survey Enterprise from hello gallery</span></span>
* <span data-ttu-id="ae20a-122">設定並測試 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ae20a-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a><span data-ttu-id="ae20a-123">從 hello 圖庫新增 IBM Kenexa 調查 Enterprise</span><span class="sxs-lookup"><span data-stu-id="ae20a-123">Add IBM Kenexa Survey Enterprise from hello gallery</span></span>
<span data-ttu-id="ae20a-124">tooconfigure hello 整合 IBM Kenexa 調查企業到 Azure AD 中，加入 IBM Kenexa 調查企業 hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae20a-124">tooconfigure hello integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ae20a-125">tooadd IBM Kenexa 調查企業 hello 圖庫中，從 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="ae20a-125">tooadd IBM Kenexa Survey Enterprise from hello gallery, do hello following:</span></span>

1. <span data-ttu-id="ae20a-126">在 [hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中按一下 hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae20a-126">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** button.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="ae20a-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ae20a-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="ae20a-130">按一下 [應用程式，tooadd hello**新的應用程式**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae20a-130">tooadd an application, click hello **New application** button.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="ae20a-132">在 [hello] 搜尋方塊中，輸入**IBM Kenexa 調查企業**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-132">In hello search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="ae20a-134">在 hello 結果清單中，選取**IBM Kenexa 調查企業**，然後按一下hello**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae20a-134">In hello results list, select **IBM Kenexa Survey Enterprise**, and then click hello **Add** button tooadd hello application.</span></span>

    ![IBM Kenexa 調查企業 hello [結果] 清單中](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ae20a-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ae20a-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ae20a-137">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 IBM Kenexa Survey Enterprise 搭配運作的 Azure AD SSO。</span><span class="sxs-lookup"><span data-stu-id="ae20a-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae20a-138">Azure AD SSO toowork tooidentify hello IBM Kenexa 調查企業使用者對應項目需要在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ae20a-138">For SSO toowork, Azure AD needs tooidentify hello IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="ae20a-139">換句話說，必須在 Azure AD 使用者和 IBM Kenexa Survey Enterprise 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ae20a-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="ae20a-140">tooestablish hello 連結關聯性，hello 分派 hello 值**使用者名**做為 hello hello 值 IBM Kenexa 調查企業中**Username**在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ae20a-140">tooestablish hello link relationship, assign hello value of hello **user name** in IBM Kenexa Survey Enterprise as hello value of hello **Username** in Azure AD.</span></span>

<span data-ttu-id="ae20a-141">tooconfigure 和測試使用 IBM Kenexa 調查 Enterprise，完整的 Azure AD SSO hello hello 下兩節中的建置組塊。</span><span class="sxs-lookup"><span data-stu-id="ae20a-141">tooconfigure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete hello building blocks in hello next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="ae20a-142">設定 Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="ae20a-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="ae20a-143">在本節中，您在 hello Azure 入口網站中啟用 Azure AD 的 SSO 和 IBM Kenexa 調查企業應用程式中設定 SSO，藉由 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ae20a-143">In this section, you enable Azure AD SSO in hello Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing hello following:</span></span>

1. <span data-ttu-id="ae20a-144">在 Azure 入口網站上 hello hello **IBM Kenexa 調查企業**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-144">In hello Azure portal, on hello **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![IBM Kenexa Survey Enterprise 設定單一登入連結][4]

2. <span data-ttu-id="ae20a-146">在 hello**單一登入**對話方塊中的，在 hello**模式**方塊中，選取**SAML 型登入**tooenable SSO。</span><span class="sxs-lookup"><span data-stu-id="ae20a-146">In hello **Single sign-on** dialog box, in hello **Mode** box, select **SAML-based Sign-on** tooenable SSO.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="ae20a-148">在 hello **IBM Kenexa 調查企業網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae20a-148">In hello **IBM Kenexa Survey Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![IBM Kenexa Survey Enterprise 網域及 URL 單一登入資訊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="ae20a-150">a.</span><span class="sxs-lookup"><span data-stu-id="ae20a-150">a.</span></span> <span data-ttu-id="ae20a-151">在 hello**識別碼**文字方塊中，輸入 URL 以 hello 下列模式：`https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="ae20a-151">In hello **Identifier** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="ae20a-152">b.</span><span class="sxs-lookup"><span data-stu-id="ae20a-152">b.</span></span> <span data-ttu-id="ae20a-153">在 hello**回覆 URL**文字方塊中，輸入 URL 以 hello 下列模式：`https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="ae20a-153">In hello **Reply URL** textbox, type a URL with hello following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ae20a-154">hello 上述值不是實際。</span><span class="sxs-lookup"><span data-stu-id="ae20a-154">hello preceding values are not real.</span></span> <span data-ttu-id="ae20a-155">更新 hello 實際識別項，回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="ae20a-155">Update them with hello actual identifier and reply URL.</span></span> <span data-ttu-id="ae20a-156">tooobtain hello 實際的值，請連絡 hello [IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-156">tooobtain hello actual values, contact hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="ae20a-157">在下**SAML 簽章憑證**，按一下 **憑證 (Base64)**，然後儲存 hello 憑證檔案 tooyour 電腦。</span><span class="sxs-lookup"><span data-stu-id="ae20a-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save hello certificate file tooyour computer.</span></span>

    ![hello 憑證 (Base64) 下載連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="ae20a-159">hello IBM Kenexa 調查企業應用程式特定的格式，這需要您 tooadd 自訂屬性對應 toohello 設定您的 SAML 權杖屬性的預期 tooreceive hello 安全性判斷提示標記語言 (SAML) 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="ae20a-159">hello IBM Kenexa Survey Enterprise application expects tooreceive hello Security Assertions Markup Language (SAML) assertions in a specific format, which requires you tooadd custom attribute mappings toohello configuration of your SAML token attributes.</span></span> <span data-ttu-id="ae20a-160">hello hello 回應 hello 使用者識別項宣告的值必須符合已設定 hello Kenexa 系統中的 SSO 識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="ae20a-160">hello value of hello user-identifier claim in hello response must match hello SSO ID that's configured in hello Kenexa system.</span></span> <span data-ttu-id="ae20a-161">toomap hello 做為 SSO 網際網路資料包通訊協定 (IDP) 您組織中適當的使用者識別碼，與 hello 搭配[IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-161">toomap hello appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="ae20a-162">根據預設，Azure AD 會設定為 hello 使用者主要名稱 (UPN) 值 hello 使用者識別項。</span><span class="sxs-lookup"><span data-stu-id="ae20a-162">By default, Azure AD sets hello user identifier as hello user principal name (UPN) value.</span></span> <span data-ttu-id="ae20a-163">您可以變更此值在 hello**屬性**索引標籤上，如下列螢幕擷取畫面的 hello 中所示。</span><span class="sxs-lookup"><span data-stu-id="ae20a-163">You can change this value on hello **Attribute** tab, as shown in hello following screenshot.</span></span> <span data-ttu-id="ae20a-164">只有在您完成 hello 正確對應之後，才 hello 整合的運作方式。</span><span class="sxs-lookup"><span data-stu-id="ae20a-164">hello integration works only after you've completed hello mapping correctly.</span></span>
    
    ![hello 使用者屬性 對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. <span data-ttu-id="ae20a-166">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ae20a-166">Click **Save**.</span></span>

    ![hello 設定單一登入儲存按鈕](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae20a-168">tooopen hello**設定登入**視窗底下**IBM Kenexa 調查企業設定**，按一下 **設定 IBM Kenexa 調查企業**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-168">tooopen hello **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![hello 設定 IBM Kenexa 調查企業連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="ae20a-170">複製 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**值 hello**快速參考**> 一節。</span><span class="sxs-lookup"><span data-stu-id="ae20a-170">Copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from hello **Quick Reference** section.</span></span>

8. <span data-ttu-id="ae20a-171">在 hello**設定登入**視窗底下**快速參考**，複製 hello**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**值。</span><span class="sxs-lookup"><span data-stu-id="ae20a-171">In hello **Configure sign-on** window, under **Quick Reference**, copy hello **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="ae20a-172">在 hello tooconfigure SSO **IBM Kenexa 調查企業**端、 傳送嗨下載**憑證 (Base64)**，**登出 URL**， **SAML 實體識別碼**，和**SAML 單一登入服務 URL**值 toohello [IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-172">tooconfigure SSO on hello **IBM Kenexa Survey Enterprise** side, send hello downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values toohello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="ae20a-173">您可以使用參照 tooa 精簡版本的這些指示 hello [Azure 入口網站](https://portal.azure.com)當您在設定 hello 應用程式的設定。</span><span class="sxs-lookup"><span data-stu-id="ae20a-173">You can refer tooa concise version of these instructions in hello [Azure portal](https://portal.azure.com) while you are setting up hello app.</span></span> <span data-ttu-id="ae20a-174">從 hello 新增 hello 應用程式之後**Active Directory** > **企業應用程式**區段中，只要按一下 hello**單一登入**索引標籤，然後再存取hello 內嵌文件，透過 hello**組態**hello 結尾區段。</span><span class="sxs-lookup"><span data-stu-id="ae20a-174">After you add hello app from hello **Active Directory** > **Enterprise Applications** section, simply click hello **single sign-on** tab, and then access hello embedded documentation through hello **Configuration** section at hello end.</span></span> <span data-ttu-id="ae20a-175">toolearn 進一步了解 hello embedded 文件功能，請參閱[Azure AD 的內嵌文件](https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-175">toolearn more about hello embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ae20a-176">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ae20a-176">Create an Azure AD test user</span></span>
<span data-ttu-id="ae20a-177">在本節中，您可以建立 hello Azure 入口網站中的測試使用者許 Simon 執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="ae20a-177">In this section, you create test user Britta Simon in hello Azure portal by doing hello following:</span></span>

![建立 Azure AD 測試使用者][100]

1. <span data-ttu-id="ae20a-179">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae20a-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae20a-181">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae20a-183">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ae20a-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae20a-185">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ae20a-185">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae20a-187">a.</span><span class="sxs-lookup"><span data-stu-id="ae20a-187">a.</span></span> <span data-ttu-id="ae20a-188">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae20a-189">b.</span><span class="sxs-lookup"><span data-stu-id="ae20a-189">b.</span></span> <span data-ttu-id="ae20a-190">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="ae20a-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="ae20a-191">c.</span><span class="sxs-lookup"><span data-stu-id="ae20a-191">c.</span></span> <span data-ttu-id="ae20a-192">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="ae20a-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="ae20a-193">d.</span><span class="sxs-lookup"><span data-stu-id="ae20a-193">d.</span></span> <span data-ttu-id="ae20a-194">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ae20a-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="ae20a-195">建立 IBM Kenexa Survey Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ae20a-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="ae20a-196">在本節中，您要在 IBM Kenexa Survey Enterprise 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ae20a-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="ae20a-197">toocreate hello IBM Kenexa 調查企業系統和它們對應 hello SSO 識別碼中的使用者，您可以使用 hello [IBM Kenexa 調查企業支援小組](https://www.ibm.com/support/home/?lnk=fcw)。</span><span class="sxs-lookup"><span data-stu-id="ae20a-197">toocreate users in hello IBM Kenexa Survey Enterprise system and map hello SSO ID for them, you can work with hello [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="ae20a-198">這個 SSO 識別碼值也應該對應從 Azure AD toohello 使用者識別碼值。</span><span class="sxs-lookup"><span data-stu-id="ae20a-198">This SSO ID value should also be mapped toohello user identifier value from Azure AD.</span></span> <span data-ttu-id="ae20a-199">您可以變更此預設設定在 hello**屬性** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ae20a-199">You can change this default setting on hello **Attribute** tab.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="ae20a-200">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ae20a-200">Assign hello Azure AD test user</span></span>

<span data-ttu-id="ae20a-201">在本節中，以啟用使用者許 Simon toouse Azure SSO 授與存取 tooIBM Kenexa 調查企業。</span><span class="sxs-lookup"><span data-stu-id="ae20a-201">In this section, you enable user Britta Simon toouse Azure SSO by granting access tooIBM Kenexa Survey Enterprise.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="ae20a-203">tooassign 使用者許 Simon tooIBM Kenexa 調查企業，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="ae20a-203">tooassign user Britta Simon tooIBM Kenexa Survey Enterprise, do hello following:</span></span>

1. <span data-ttu-id="ae20a-204">在 hello Azure 入口網站，開啟 hello**應用程式**檢視，請進入 toohello**目錄**檢視中，選取**企業應用程式**，然後按一下**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-204">In hello Azure portal, open hello **Applications** view, go toohello **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![hello [企業應用程式] 和 [所有應用程式] 連結][201] 

2. <span data-ttu-id="ae20a-206">在 hello**應用程式**清單中，選取**IBM Kenexa 調查企業**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-206">In hello **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![hello 應用程式清單中的 hello IBM Kenexa 調查企業連結](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="ae20a-208">在 hello 左窗格中，按一下 **使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-208">In hello left pane, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="ae20a-210">按一下 hello**新增** 按鈕，然後在 hello**將作業加入**窗格中，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-210">Click hello **Add** button and then, in hello **Add Assignment** pane, select **Users and groups**.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="ae20a-212">在 hello**使用者和群組**對話方塊中的，在 hello**使用者**清單中，選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="ae20a-212">In hello **Users and groups** dialog box, in hello **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ae20a-213">在 [hello**使用者和群組**對話方塊方塊中，按一下 hello**選取**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae20a-213">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="ae20a-214">在 [hello**將作業加入**對話方塊方塊中，按一下 hello**指派**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ae20a-214">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ae20a-215">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ae20a-215">Test single sign-on</span></span>

<span data-ttu-id="ae20a-216">本節中，在中，您可以測試您的 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ae20a-216">In this section, you test your Azure AD SSO configuration by using hello Access Panel.</span></span>

<span data-ttu-id="ae20a-217">當您按一下 hello **IBM Kenexa 調查企業**以並排顯示 hello 存取面板中，您應該自動登入 tooyour IBM Kenexa 調查企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="ae20a-217">When you click hello **IBM Kenexa Survey Enterprise** tile in hello Access Panel, you should be automatically signed in tooyour IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae20a-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="ae20a-218">Additional resources</span></span>

* [<span data-ttu-id="ae20a-219">如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae20a-219">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae20a-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ae20a-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
