---
title: "教學課程：Azure Active Directory 與 Netsuite 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Netsuite 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dafa0864-aef2-4f5e-9eac-770504688ef4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 7cf205d5bda5333872fb589e57f4779a8670b595
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netsuite"></a><span data-ttu-id="ccfcb-103">教學課程：Azure Active Directory 與 Netsuite 整合</span><span class="sxs-lookup"><span data-stu-id="ccfcb-103">Tutorial: Azure Active Directory integration with Netsuite</span></span>

<span data-ttu-id="ccfcb-104">在此教學課程中，您學會如何 toointegrate Netsuite 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-104">In this tutorial, you learn how toointegrate Netsuite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ccfcb-105">與 Azure AD 整合 Netsuite 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="ccfcb-105">Integrating Netsuite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ccfcb-106">您可以控制存取 tooNetsuite Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="ccfcb-106">You can control in Azure AD who has access tooNetsuite</span></span>
- <span data-ttu-id="ccfcb-107">您可以啟用您的使用者 tooautomatically get 登入 tooNetsuite （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="ccfcb-107">You can enable your users tooautomatically get signed-on tooNetsuite (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ccfcb-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ccfcb-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ccfcb-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccfcb-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ccfcb-110">Prerequisites</span></span>

<span data-ttu-id="ccfcb-111">tooconfigure 與 Netsuite 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="ccfcb-111">tooconfigure Azure AD integration with Netsuite, you need hello following items:</span></span>

- <span data-ttu-id="ccfcb-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ccfcb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ccfcb-113">啟用 Netsuite 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ccfcb-113">A Netsuite single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ccfcb-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ccfcb-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ccfcb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ccfcb-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ccfcb-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ccfcb-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ccfcb-118">Scenario description</span></span>
<span data-ttu-id="ccfcb-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ccfcb-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="ccfcb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ccfcb-121">從 hello 圖庫加入 Netsuite</span><span class="sxs-lookup"><span data-stu-id="ccfcb-121">Adding Netsuite from hello gallery</span></span>
2. <span data-ttu-id="ccfcb-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ccfcb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netsuite-from-hello-gallery"></a><span data-ttu-id="ccfcb-123">從 hello 圖庫加入 Netsuite</span><span class="sxs-lookup"><span data-stu-id="ccfcb-123">Adding Netsuite from hello gallery</span></span>
<span data-ttu-id="ccfcb-124">tooconfigure hello 整合 Netsuite 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Netsuite。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-124">tooconfigure hello integration of Netsuite into Azure AD, you need tooadd Netsuite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ccfcb-125">**tooadd Netsuite 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ccfcb-125">**tooadd Netsuite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccfcb-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ccfcb-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ccfcb-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ccfcb-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ccfcb-133">在 [hello] 搜尋方塊中，輸入**Netsuite**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-133">In hello search box, type **Netsuite**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_search.png)

5. <span data-ttu-id="ccfcb-135">在 hello 結果 窗格中，選取  **Netsuite**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-135">In hello results panel, select **Netsuite**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ccfcb-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ccfcb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ccfcb-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Netsuite 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-138">In this section, you configure and test Azure AD single sign-on with Netsuite based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ccfcb-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Netsuite 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Netsuite is tooa user in Azure AD.</span></span> <span data-ttu-id="ccfcb-140">換句話說，Azure AD 使用者與 hello Netsuite 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-140">In other words, a link relationship between an Azure AD user and hello related user in Netsuite needs toobe established.</span></span>

<span data-ttu-id="ccfcb-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Netsuite 中。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Netsuite.</span></span>

<span data-ttu-id="ccfcb-142">tooconfigure 及測試 Azure AD 單一登入 Netsuite，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="ccfcb-142">tooconfigure and test Azure AD single sign-on with Netsuite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ccfcb-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ccfcb-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ccfcb-145">**[建立測試使用者 Netsuite](#creating-a-netsuite-test-user)**  -toohave 許 Simon Netsuite 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-145">**[Creating a Netsuite test user](#creating-a-netsuite-test-user)** - toohave a counterpart of Britta Simon in Netsuite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ccfcb-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ccfcb-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ccfcb-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ccfcb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ccfcb-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 Netsuite 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Netsuite application.</span></span>

<span data-ttu-id="ccfcb-150">**tooconfigure Azure AD 單一登入 Netsuite，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ccfcb-150">**tooconfigure Azure AD single sign-on with Netsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccfcb-151">在 Azure 入口網站上 hello hello **Netsuite**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-151">In hello Azure portal, on hello **Netsuite** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ccfcb-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_samlbase.png)

3. <span data-ttu-id="ccfcb-155">在 hello **Netsuite 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ccfcb-155">On hello **Netsuite Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_url.png)

    <span data-ttu-id="ccfcb-157">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello: `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs``https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span><span class="sxs-lookup"><span data-stu-id="ccfcb-157">In hello **Reply URL** textbox, type a URL using hello following pattern:   `https://<tenant-name>.netsuite.com/saml2/acs` `https://<tenant-name>.na1.netsuite.com/saml2/acs` `https://<tenant-name>.na2.netsuite.com/saml2/acs` `https://<tenant-name>.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na1.sandbox.netsuite.com/saml2/acs` `https://<tenant-name>.na2.sandbox.netsuite.com/saml2/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ccfcb-158">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-158">This value is not real value.</span></span> <span data-ttu-id="ccfcb-159">更新 hello 值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-159">Update hello value with hello actual Reply URL.</span></span> <span data-ttu-id="ccfcb-160">請連絡[Netsuite 支援小組](http://www.netsuite.com/portal/services/support.shtml)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-160">Contact [Netsuite support team](http://www.netsuite.com/portal/services/support.shtml) tooget this value.</span></span>
 
4. <span data-ttu-id="ccfcb-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_certificate.png) 

5. <span data-ttu-id="ccfcb-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ccfcb-165">在 hello **Netsuite 設定**區段中，按一下**設定 Netsuite** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-165">On hello **Netsuite Configuration** section, click **Configure Netsuite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ccfcb-166">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="ccfcb-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_configure.png) 

7. <span data-ttu-id="ccfcb-168">在瀏覽器中開啟新索引標籤，以系統管理員的身分登入您的 Netsuite 公司站台。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-168">Open a new tab in your browser, and sign into your Netsuite company site as an administrator.</span></span>

8. <span data-ttu-id="ccfcb-169">在 hello hello hello 頁頂端的工具列中按一下**安裝**，然後按一下 **安裝管理員**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-169">In hello toolbar at hello top of hello page, click **Setup**, then click **Setup Manager**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

9. <span data-ttu-id="ccfcb-171">從 hello**安裝工作**清單中，選取**整合**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-171">From hello **Setup Tasks** list, select **Integration**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-integration.png)

10. <span data-ttu-id="ccfcb-173">在 hello**管理驗證**區段中，按一下**SAML 單一登入**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-173">In hello **Manage Authentication** section, click **SAML Single Sign-on**.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-saml.png)

11. <span data-ttu-id="ccfcb-175">在 hello **SAML 設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ccfcb-175">On hello **SAML Setup** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="ccfcb-176">a.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-176">a.</span></span> <span data-ttu-id="ccfcb-177">複製 hello **SAML 單一登入服務 URL**值**快速參考**區段**設定登入**並將它貼到 hello**身分識別提供者登入頁面**Netsuite 欄位。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-177">Copy hello **SAML Single Sign-On Service URL** value from **Quick Reference** section of **Configure sign-on** and paste it into hello **Identity Provider Login Page** field in Netsuite.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/ns-saml-setup.png)
  
    <span data-ttu-id="ccfcb-179">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-179">b.</span></span> <span data-ttu-id="ccfcb-180">在 Netsuite 中，選取 [主要驗證方法] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-180">In Netsuite, select **Primary Authentication Method**.</span></span>

    <span data-ttu-id="ccfcb-181">c.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-181">c.</span></span> <span data-ttu-id="ccfcb-182">Hello 欄位標示為**SAMLV2 身分識別提供者中繼資料**，選取**上傳 IDP 中繼資料檔案**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-182">For hello field labeled **SAMLV2 Identity Provider Metadata**, select **Upload IDP Metadata File**.</span></span> <span data-ttu-id="ccfcb-183">然後按一下 **瀏覽**tooupload hello 中繼資料檔從 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-183">Then click **Browse** tooupload hello metadata file that you downloaded from Azure portal.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/ns-sso-setup.png)

    <span data-ttu-id="ccfcb-185">d.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-185">d.</span></span> <span data-ttu-id="ccfcb-186">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-186">Click **Submit**.</span></span>

12. <span data-ttu-id="ccfcb-187">在 Azure AD 中，按一下 [檢視及編輯所有其他使用者屬性] 核取方塊並新增屬性。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-187">In Azure AD, Click on **View and edit all other user attributes** check-box and add attribute.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-attributes.png)

13. <span data-ttu-id="ccfcb-189">Hello**屬性名稱**欄位中，輸入`account`。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-189">For hello **Attribute Name** field, type in `account`.</span></span> <span data-ttu-id="ccfcb-190">Hello**屬性值**欄位中，輸入您的 Netsuite 帳戶識別碼。這個值是常數，而與帳戶的變更。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-190">For hello **Attribute Value** field, type in your Netsuite account ID.This value is constant and change with account.</span></span> <span data-ttu-id="ccfcb-191">指示如何 toofind 列入您的帳戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="ccfcb-191">Instructions on how toofind your account ID are included below:</span></span>

      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-add-attribute.png)

    <span data-ttu-id="ccfcb-193">a.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-193">a.</span></span> <span data-ttu-id="ccfcb-194">在 Netsuite，按一下 **安裝**hello 上方瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-194">In Netsuite, click **Setup** from hello top navigation menu.</span></span>

    <span data-ttu-id="ccfcb-195">b.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-195">b.</span></span> <span data-ttu-id="ccfcb-196">然後按一下 下 hello**安裝工作**區段 hello 左的導覽功能表上，選取 hello**整合**區段，然後按一下  **Web 服務喜好設定**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-196">Then click under hello **Setup Tasks** section of hello left navigation menu, select hello **Integration** section, and click **Web Services Preferences**.</span></span>

    <span data-ttu-id="ccfcb-197">c.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-197">c.</span></span> <span data-ttu-id="ccfcb-198">複製您 Netsuite 的帳戶識別碼，並將它貼到 hello**屬性值**在 Azure AD 中的欄位。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-198">Copy your Netsuite Account ID and paste it into hello **Attribute Value** field in Azure AD.</span></span>

    ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-account-id.png)

14. <span data-ttu-id="ccfcb-200">使用者可以執行單一登入 Netsuite 之前，必須先指派 hello Netsuite 中的適當權限。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-200">Before users can perform single sign-on into Netsuite, they must first be assigned hello appropriate permissions in Netsuite.</span></span> <span data-ttu-id="ccfcb-201">請遵循以下 tooassign hello 指示這些權限。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-201">Follow hello instructions below tooassign these permissions.</span></span>

    <span data-ttu-id="ccfcb-202">a.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-202">a.</span></span> <span data-ttu-id="ccfcb-203">在 hello 頂端導覽功能表上，按一下 **安裝**，然後按一下 **安裝管理員**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-203">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="ccfcb-205">b.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-205">b.</span></span> <span data-ttu-id="ccfcb-206">在 hello 左的導覽功能表上，選取 **使用者/角色**，然後按一下 **管理角色**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-206">On hello left navigation menu, select **Users/Roles**, then click **Manage Roles**.</span></span>
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-manage-roles.png)

    <span data-ttu-id="ccfcb-208">c.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-208">c.</span></span> <span data-ttu-id="ccfcb-209">按一下 [新角色] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-209">Click **New Role**.</span></span>

    <span data-ttu-id="ccfcb-210">d.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-210">d.</span></span> <span data-ttu-id="ccfcb-211">在中輸入**名稱**新角色，及選取 hello**單一登入只**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-211">Type in a **Name** for your new role, and select hello **Single Sign-On Only** checkbox.</span></span>
      
      ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-new-role.png)

    <span data-ttu-id="ccfcb-213">e.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-213">e.</span></span> <span data-ttu-id="ccfcb-214">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-214">Click **Save**.</span></span>

    <span data-ttu-id="ccfcb-215">f.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-215">f.</span></span> <span data-ttu-id="ccfcb-216">在 hello 最上層顯示 hello 功能表上，按一下**權限**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-216">In hello menu on hello top, click **Permissions**.</span></span> <span data-ttu-id="ccfcb-217">然後按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-217">Then click **Setup**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-sso.png)

    <span data-ttu-id="ccfcb-219">g.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-219">g.</span></span> <span data-ttu-id="ccfcb-220">選取 設定 SAM 單一登入，然後按一下新增。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-220">Select **Set Up SAM Single Sign-on**, and then click **Add**.</span></span>

    <span data-ttu-id="ccfcb-221">h.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-221">h.</span></span> <span data-ttu-id="ccfcb-222">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-222">Click **Save**.</span></span>

    <span data-ttu-id="ccfcb-223">i.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-223">i.</span></span> <span data-ttu-id="ccfcb-224">在 hello 頂端導覽功能表上，按一下 **安裝**，然後按一下 **安裝管理員**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-224">On hello top navigation menu, click **Setup**, then click **Setup Manager**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-setup.png)

    <span data-ttu-id="ccfcb-226">j.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-226">j.</span></span> <span data-ttu-id="ccfcb-227">在 hello 左的導覽功能表上，選取 **使用者/角色**，然後按一下 **管理使用者**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-227">On hello left navigation menu, select **Users/Roles**, then click **Manage Users**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-manage-users.png)

    <span data-ttu-id="ccfcb-229">k.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-229">k.</span></span> <span data-ttu-id="ccfcb-230">選取測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-230">Select a test user.</span></span> <span data-ttu-id="ccfcb-231">然後按一下 [編輯] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-231">Then click **Edit**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-edit-user.png)

    <span data-ttu-id="ccfcb-233">l.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-233">l.</span></span> <span data-ttu-id="ccfcb-234">在 hello 角色對話方塊中，選取 hello 角色，您已建立，並按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-234">On hello Roles dialog, select hello role that you have created and click **Add**.</span></span>
      
       ![設定單一登入](./media/active-directory-saas-Netsuite-tutorial/ns-add-role.png)

    <span data-ttu-id="ccfcb-236">m.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-236">m.</span></span> <span data-ttu-id="ccfcb-237">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-237">Click **Save**.</span></span>
    
> [!TIP]
> <span data-ttu-id="ccfcb-238">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="ccfcb-238">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ccfcb-239">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-239">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ccfcb-240">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ccfcb-240">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ccfcb-241">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ccfcb-241">Creating an Azure AD test user</span></span>
<span data-ttu-id="ccfcb-242">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-242">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ccfcb-244">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ccfcb-244">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccfcb-245">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-245">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="ccfcb-247">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-247">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ccfcb-249">在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-249">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ccfcb-251">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="ccfcb-251">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-netsuite-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ccfcb-253">a.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-253">a.</span></span> <span data-ttu-id="ccfcb-254">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-254">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ccfcb-255">b.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-255">b.</span></span> <span data-ttu-id="ccfcb-256">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-256">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ccfcb-257">c.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-257">c.</span></span> <span data-ttu-id="ccfcb-258">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-258">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ccfcb-259">d.</span><span class="sxs-lookup"><span data-stu-id="ccfcb-259">d.</span></span> <span data-ttu-id="ccfcb-260">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-260">Click **Create**.</span></span> 

### <a name="creating-a-netsuite-test-user"></a><span data-ttu-id="ccfcb-261">建立 Netsuite 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ccfcb-261">Creating a Netsuite test user</span></span>

<span data-ttu-id="ccfcb-262">本節會在 Netsuite 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-262">In this section, a user called Britta Simon is created in Netsuite.</span></span> <span data-ttu-id="ccfcb-263">Netsuite 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-263">Netsuite supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="ccfcb-264">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-264">There is no action item for you in this section.</span></span> <span data-ttu-id="ccfcb-265">如果使用者不存在於 Netsuite，當您嘗試 tooaccess Netsuite 時，會建立一個新。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-265">If a user doesn't already exist in Netsuite, a new one is created when you attempt tooaccess Netsuite.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ccfcb-266">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="ccfcb-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ccfcb-267">在本節中，您可以授與存取 tooNetsuite 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetsuite.</span></span>

![指派使用者][200] 

<span data-ttu-id="ccfcb-269">**tooassign 許 Simon tooNetsuite，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="ccfcb-269">**tooassign Britta Simon tooNetsuite, perform hello following steps:**</span></span>

1. <span data-ttu-id="ccfcb-270">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ccfcb-272">在 [hello] 應用程式清單中，選取**Netsuite**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-272">In hello applications list, select **Netsuite**.</span></span>

    ![設定單一登入](./media/active-directory-saas-netsuite-tutorial/tutorial_netsuite_app.png) 

3. <span data-ttu-id="ccfcb-274">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ccfcb-276">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-276">Click **Add** button.</span></span> <span data-ttu-id="ccfcb-277">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ccfcb-279">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ccfcb-280">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ccfcb-281">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ccfcb-282">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ccfcb-282">Testing single sign-on</span></span>

<span data-ttu-id="ccfcb-283">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ccfcb-284">您的單一登入設定，開啟 hello 存取面板的 tootest [https://myapps.microsoft.com](https://myapps.microsoft.com/)，登入 hello 測試帳戶，然後按一下**Netsuite**。</span><span class="sxs-lookup"><span data-stu-id="ccfcb-284">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), sign into hello test account, and click **Netsuite**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ccfcb-285">其他資源</span><span class="sxs-lookup"><span data-stu-id="ccfcb-285">Additional resources</span></span>

* [<span data-ttu-id="ccfcb-286">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ccfcb-286">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ccfcb-287">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ccfcb-287">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="ccfcb-288">設定使用者佈建</span><span class="sxs-lookup"><span data-stu-id="ccfcb-288">Configure User Provisioning</span></span>](active-directory-saas-netsuite-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netsuite-tutorial/tutorial_general_203.png

