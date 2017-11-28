---
title: "教學課程：Azure Active Directory 與 Zendesk 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zendesk 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="0698e-103">教學課程：Azure Active Directory 與 Zendesk 整合</span><span class="sxs-lookup"><span data-stu-id="0698e-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="0698e-104">在此教學課程中，您學會如何 toointegrate Zendesk 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0698e-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0698e-105">整合 Azure AD 與 Zendesk 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="0698e-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0698e-106">您可以控制存取 tooZendesk Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="0698e-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="0698e-107">您可以啟用您的使用者 tooautomatically get 登入 tooZendesk （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="0698e-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0698e-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0698e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0698e-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0698e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0698e-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0698e-110">Prerequisites</span></span>

<span data-ttu-id="0698e-111">tooconfigure Azure AD 與 Zendesk 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0698e-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="0698e-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0698e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0698e-113">已啟用 Zendesk 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0698e-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="0698e-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0698e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="0698e-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0698e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0698e-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0698e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0698e-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="0698e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="0698e-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0698e-118">Scenario description</span></span>
<span data-ttu-id="0698e-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0698e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0698e-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0698e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0698e-121">從 hello 圖庫加入 Zendesk</span><span class="sxs-lookup"><span data-stu-id="0698e-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="0698e-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0698e-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="0698e-123">從 hello 圖庫加入 Zendesk</span><span class="sxs-lookup"><span data-stu-id="0698e-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="0698e-124">tooconfigure hello 整合 Zendesk 的 Azure AD，您需要 tooadd Zendesk hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0698e-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0698e-125">**tooadd Zendesk hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0698e-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0698e-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0698e-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0698e-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0698e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0698e-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0698e-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="0698e-131">按一下**新的應用程式**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0698e-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="0698e-133">在 [hello] 搜尋方塊中，輸入**Zendesk**。</span><span class="sxs-lookup"><span data-stu-id="0698e-133">In hello search box, type **Zendesk**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="0698e-135">在 hello 結果 窗格中，選取  **Zendesk**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0698e-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0698e-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0698e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0698e-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Zendesk 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0698e-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0698e-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Zendesk 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0698e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="0698e-140">換句話說，Azure AD 使用者與 hello Zendesk 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0698e-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="0698e-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Zendesk 中。</span><span class="sxs-lookup"><span data-stu-id="0698e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="0698e-142">tooconfigure 及 Azure AD 單一登入與 Zendesk 的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0698e-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0698e-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0698e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0698e-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0698e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0698e-145">**[建立測試使用者 Zendesk](#creating-a-zendesk-test-user)**  -toohave 許 Simon 是表示連結的 toohello Azure AD 使用者的 Zendesk 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="0698e-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0698e-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0698e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0698e-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0698e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0698e-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0698e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0698e-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 Zendesk 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="0698e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="0698e-150">**tooconfigure Azure AD 單一登入與 Zendesk，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0698e-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="0698e-151">在 Azure 入口網站上 hello hello **Zendesk**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0698e-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="0698e-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0698e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="0698e-155">在 hello **Zendesk 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0698e-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="0698e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0698e-157">a.</span></span> <span data-ttu-id="0698e-158">在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="0698e-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="0698e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0698e-159">b.</span></span> <span data-ttu-id="0698e-160">在 hello**識別碼**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="0698e-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0698e-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0698e-161">These values are not real.</span></span> <span data-ttu-id="0698e-162">更新這些值與 hello 實際登入 URL 和識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="0698e-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="0698e-163">請連絡[Zendesk 支援小組](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="0698e-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="0698e-164">Zendesk 預期 hello SAML 判斷提示，以特定格式。</span><span class="sxs-lookup"><span data-stu-id="0698e-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0698e-165">沒有強制 SAML 屬性，但您可以選擇新增屬性從**使用者屬性**區段由下列 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0698e-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="0698e-167">a.</span><span class="sxs-lookup"><span data-stu-id="0698e-167">a.</span></span> <span data-ttu-id="0698e-168">按一下 hello**檢視及編輯所有 hello 其他屬性**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="0698e-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="0698e-170">b.</span><span class="sxs-lookup"><span data-stu-id="0698e-170">b.</span></span> <span data-ttu-id="0698e-171">按一下 hello**加入屬性**tooopen**加入屬性**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0698e-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="0698e-173">c.</span><span class="sxs-lookup"><span data-stu-id="0698e-173">c.</span></span> <span data-ttu-id="0698e-174">在 hello**名稱**文字方塊中，型別 hello 屬性名稱 (例如**emailaddress**)。</span><span class="sxs-lookup"><span data-stu-id="0698e-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="0698e-175">d.</span><span class="sxs-lookup"><span data-stu-id="0698e-175">d.</span></span> <span data-ttu-id="0698e-176">從 hello**值**清單，選取 hello 屬性值 (做為**user.mail**)。</span><span class="sxs-lookup"><span data-stu-id="0698e-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="0698e-177">e.</span><span class="sxs-lookup"><span data-stu-id="0698e-177">e.</span></span> <span data-ttu-id="0698e-178">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="0698e-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="0698e-179">您使用不在預設的 Azure AD 中的擴充功能屬性 tooadd 屬性。</span><span class="sxs-lookup"><span data-stu-id="0698e-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="0698e-180">按一下[使用者屬性可以設定在 SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello 的完整清單 SAML 屬性 (attribute) **Zendesk**接受。</span><span class="sxs-lookup"><span data-stu-id="0698e-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="0698e-181">在 hello **SAML 簽章憑證**區段，複製 hello**指紋**憑證值。</span><span class="sxs-lookup"><span data-stu-id="0698e-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="0698e-183">在 hello **Zendesk 組態**區段中，按一下**設定 Zendesk** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="0698e-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0698e-184">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="0698e-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="0698e-186">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zendesk 公司網站。</span><span class="sxs-lookup"><span data-stu-id="0698e-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="0698e-187">按一下 Admin 。</span><span class="sxs-lookup"><span data-stu-id="0698e-187">Click **Admin**.</span></span>

9. <span data-ttu-id="0698e-188">在 hello 左側瀏覽窗格中，按一下 **設定**，然後按一下**安全性**。</span><span class="sxs-lookup"><span data-stu-id="0698e-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="0698e-189">在 hello**安全性**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0698e-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="0698e-190">![安全性](./media/active-directory-saas-zendesk-tutorial/ic773089.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="0698e-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="0698e-191">![單一登入](./media/active-directory-saas-zendesk-tutorial/ic773090.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="0698e-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="0698e-192">a.</span><span class="sxs-lookup"><span data-stu-id="0698e-192">a.</span></span> <span data-ttu-id="0698e-193">按一下 hello**系統管理員和代理程式** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0698e-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="0698e-194">b.</span><span class="sxs-lookup"><span data-stu-id="0698e-194">b.</span></span> <span data-ttu-id="0698e-195">選取 [單一登入 (SSO) 和 SAML]，然後選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="0698e-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="0698e-196">c.</span><span class="sxs-lookup"><span data-stu-id="0698e-196">c.</span></span> <span data-ttu-id="0698e-197">在**SAML SSO URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="0698e-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="0698e-198">d.</span><span class="sxs-lookup"><span data-stu-id="0698e-198">d.</span></span> <span data-ttu-id="0698e-199">在**遠端登出 URL**文字方塊中，貼上 hello 值**登出 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="0698e-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="0698e-200">e.</span><span class="sxs-lookup"><span data-stu-id="0698e-200">e.</span></span> <span data-ttu-id="0698e-201">在**憑證指紋**文字方塊中，貼上 hello**指紋**憑證，您從 Azure 入口網站複製的值。</span><span class="sxs-lookup"><span data-stu-id="0698e-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="0698e-202">f.</span><span class="sxs-lookup"><span data-stu-id="0698e-202">f.</span></span> <span data-ttu-id="0698e-203">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="0698e-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0698e-204">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0698e-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="0698e-205">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0698e-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="0698e-207">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0698e-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0698e-208">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0698e-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0698e-210">使用者 toodisplay hello 清單太移**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0698e-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0698e-212">在 hello hello 對話方塊頂端，按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0698e-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0698e-214">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0698e-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0698e-216">a.</span><span class="sxs-lookup"><span data-stu-id="0698e-216">a.</span></span> <span data-ttu-id="0698e-217">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0698e-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0698e-218">b.</span><span class="sxs-lookup"><span data-stu-id="0698e-218">b.</span></span> <span data-ttu-id="0698e-219">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="0698e-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0698e-220">c.</span><span class="sxs-lookup"><span data-stu-id="0698e-220">c.</span></span> <span data-ttu-id="0698e-221">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="0698e-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0698e-222">d.</span><span class="sxs-lookup"><span data-stu-id="0698e-222">d.</span></span> <span data-ttu-id="0698e-223">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0698e-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="0698e-224">建立 Zendesk 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0698e-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="0698e-225">到 tooenable Azure AD 使用者 toolog **Zendesk**，您必須佈建到**Zendesk**。</span><span class="sxs-lookup"><span data-stu-id="0698e-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="0698e-226">Hello 角色指派 hello 應用程式中，根據它的 hello 預期的行為：</span><span class="sxs-lookup"><span data-stu-id="0698e-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="0698e-227">[使用者] 帳戶會在登入時自動佈建。</span><span class="sxs-lookup"><span data-stu-id="0698e-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="0698e-228">**代理程式**和**Admin**帳戶需要手動佈建中 toobe **Zendesk**登入。</span><span class="sxs-lookup"><span data-stu-id="0698e-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="0698e-229">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0698e-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0698e-230">登入 tooyour **Zendesk**租用戶。</span><span class="sxs-lookup"><span data-stu-id="0698e-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="0698e-231">選取 hello**客戶清單** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="0698e-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="0698e-232">選取 hello**使用者**索引標籤，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="0698e-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="0698e-233">![新增使用者](./media/active-directory-saas-zendesk-tutorial/ic773632.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="0698e-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="0698e-234">輸入現有 Azure AD 帳戶 tooprovision，然後再按一下 hello 電子郵件地址**儲存**。</span><span class="sxs-lookup"><span data-stu-id="0698e-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="0698e-235">![新增使用者](./media/active-directory-saas-zendesk-tutorial/ic773633.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="0698e-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="0698e-236">您可以使用任何其他 Zendesk 使用者帳戶建立工具或 Api 提供 Zendesk tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="0698e-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0698e-237">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="0698e-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0698e-238">在本節中，您可以授與存取 tooZendesk 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0698e-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![指派使用者][200] 

<span data-ttu-id="0698e-240">**tooassign 許 Simon tooZendesk，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0698e-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="0698e-241">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0698e-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0698e-243">在 [hello] 應用程式清單中，選取**Zendesk**。</span><span class="sxs-lookup"><span data-stu-id="0698e-243">In hello applications list, select **Zendesk**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="0698e-245">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0698e-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="0698e-247">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0698e-247">Click **Add** button.</span></span> <span data-ttu-id="0698e-248">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0698e-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="0698e-250">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="0698e-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0698e-251">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0698e-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0698e-252">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0698e-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0698e-253">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0698e-253">Testing single sign-on</span></span>

<span data-ttu-id="0698e-254">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0698e-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0698e-255">當您按一下 hello Zendesk 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Zendesk 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0698e-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="0698e-256">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="0698e-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0698e-257">其他資源</span><span class="sxs-lookup"><span data-stu-id="0698e-257">Additional resources</span></span>

* [<span data-ttu-id="0698e-258">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0698e-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0698e-259">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0698e-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
