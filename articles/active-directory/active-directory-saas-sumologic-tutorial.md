---
title: "教學課程：Azure Active Directory 與 SumoLogic 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SumoLogic 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 2ef1bd329f5db8899f0b57744e4c0f6eed1c532f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="8c00b-103">教學課程：Azure Active Directory 與 SumoLogic 整合</span><span class="sxs-lookup"><span data-stu-id="8c00b-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="8c00b-104">在此教學課程中，您學會如何 toointegrate SumoLogic 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="8c00b-104">In this tutorial, you learn how toointegrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8c00b-105">整合 Azure AD 與 SumoLogic 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-105">Integrating SumoLogic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8c00b-106">您可以控制存取 tooSumoLogic Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="8c00b-106">You can control in Azure AD who has access tooSumoLogic</span></span>
- <span data-ttu-id="8c00b-107">您可以啟用您的使用者 tooautomatically get 登入 tooSumoLogic （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="8c00b-107">You can enable your users tooautomatically get signed-on tooSumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8c00b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8c00b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8c00b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="8c00b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c00b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="8c00b-110">Prerequisites</span></span>

<span data-ttu-id="8c00b-111">tooconfigure Azure AD 與 SumoLogic 的整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-111">tooconfigure Azure AD integration with SumoLogic, you need hello following items:</span></span>

- <span data-ttu-id="8c00b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8c00b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8c00b-113">已啟用 SumoLogic 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="8c00b-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8c00b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="8c00b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8c00b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="8c00b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8c00b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="8c00b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8c00b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="8c00b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8c00b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="8c00b-118">Scenario description</span></span>
<span data-ttu-id="8c00b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8c00b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8c00b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="8c00b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8c00b-121">從 hello 圖庫加入 SumoLogic</span><span class="sxs-lookup"><span data-stu-id="8c00b-121">Adding SumoLogic from hello gallery</span></span>
2. <span data-ttu-id="8c00b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8c00b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-hello-gallery"></a><span data-ttu-id="8c00b-123">從 hello 圖庫加入 SumoLogic</span><span class="sxs-lookup"><span data-stu-id="8c00b-123">Adding SumoLogic from hello gallery</span></span>
<span data-ttu-id="8c00b-124">tooconfigure hello 整合 SumoLogic 的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd SumoLogic。</span><span class="sxs-lookup"><span data-stu-id="8c00b-124">tooconfigure hello integration of SumoLogic into Azure AD, you need tooadd SumoLogic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8c00b-125">**tooadd SumoLogic 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8c00b-125">**tooadd SumoLogic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c00b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8c00b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8c00b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8c00b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="8c00b-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="8c00b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="8c00b-133">在 [hello] 搜尋方塊中，輸入**SumoLogic**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-133">In hello search box, type **SumoLogic**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="8c00b-135">在 hello 結果 窗格中，選取  **SumoLogic**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c00b-135">In hello results panel, select **SumoLogic**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8c00b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8c00b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8c00b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 SumoLogic 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8c00b-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8c00b-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 SumoLogic 中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="8c00b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SumoLogic is tooa user in Azure AD.</span></span> <span data-ttu-id="8c00b-140">換句話說，Azure AD 使用者與 hello SumoLogic 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="8c00b-140">In other words, a link relationship between an Azure AD user and hello related user in SumoLogic needs toobe established.</span></span>

<span data-ttu-id="8c00b-141">在 SumoLogic 中，將指派的 hello hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="8c00b-141">In SumoLogic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8c00b-142">tooconfigure 及測試 Azure AD 單一登入 SumoLogic，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-142">tooconfigure and test Azure AD single sign-on with SumoLogic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8c00b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="8c00b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8c00b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="8c00b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8c00b-145">**[建立測試使用者 SumoLogic](#creating-a-sumologic-test-user)**  -toohave 許 Simon SumoLogic 所連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="8c00b-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - toohave a counterpart of Britta Simon in SumoLogic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8c00b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8c00b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8c00b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="8c00b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8c00b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="8c00b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8c00b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 SumoLogic 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="8c00b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="8c00b-150">**tooconfigure Azure AD 單一登入與 SumoLogic，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8c00b-150">**tooconfigure Azure AD single sign-on with SumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c00b-151">在 Azure 入口網站上 hello hello **SumoLogic**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-151">In hello Azure portal, on hello **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="8c00b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8c00b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="8c00b-155">在 hello **SumoLogic 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-155">On hello **SumoLogic Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="8c00b-157">a.</span><span class="sxs-lookup"><span data-stu-id="8c00b-157">a.</span></span> <span data-ttu-id="8c00b-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="8c00b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="8c00b-159">b.</span><span class="sxs-lookup"><span data-stu-id="8c00b-159">b.</span></span> <span data-ttu-id="8c00b-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="8c00b-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="8c00b-161">These values are not real.</span></span> <span data-ttu-id="8c00b-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="8c00b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8c00b-163">請連絡[SumoLogic 用戶端支援小組](https://www.sumologic.com/contact-us/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="8c00b-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="8c00b-164">在 hello **SAML 簽章憑證**區段中，按一下**憑證 (Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="8c00b-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="8c00b-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8c00b-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8c00b-168">在 hello **SumoLogic 組態**區段中，按一下**設定 SumoLogic** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="8c00b-168">On hello **SumoLogic Configuration** section, click **Configure SumoLogic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8c00b-169">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="8c00b-169">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="8c00b-171">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour SumoLogic 公司網站。</span><span class="sxs-lookup"><span data-stu-id="8c00b-171">In a different web browser window, log in tooyour SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="8c00b-172">跳過**管理\>安全性**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-172">Go too**Manage \> Security**.</span></span>
   
    <span data-ttu-id="8c00b-173">![管理](./media/active-directory-saas-sumologic-tutorial/ic778556.png "管理")</span><span class="sxs-lookup"><span data-stu-id="8c00b-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="8c00b-174">按一下 [SAML] 。</span><span class="sxs-lookup"><span data-stu-id="8c00b-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="8c00b-175">![全域安全性設定](./media/active-directory-saas-sumologic-tutorial/ic778557.png "全域安全性設定")</span><span class="sxs-lookup"><span data-stu-id="8c00b-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="8c00b-176">從 hello**選取組態或建立一個新**清單中，選取**Azure AD**，然後按一下**設定**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-176">From hello **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="8c00b-177">![設定 SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "設定 SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="8c00b-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="8c00b-178">在 [hello**設定 SAML 2.0** ] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-178">On hello **Configure SAML 2.0** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="8c00b-179">![設定 SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "設定 SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="8c00b-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="8c00b-180">a.</span><span class="sxs-lookup"><span data-stu-id="8c00b-180">a.</span></span> <span data-ttu-id="8c00b-181">在 hello**組態名稱**文字方塊中，輸入**Azure AD**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-181">In hello **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="8c00b-182">b.</span><span class="sxs-lookup"><span data-stu-id="8c00b-182">b.</span></span> <span data-ttu-id="8c00b-183">選取 [偵錯模式] 。</span><span class="sxs-lookup"><span data-stu-id="8c00b-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="8c00b-184">c.</span><span class="sxs-lookup"><span data-stu-id="8c00b-184">c.</span></span> <span data-ttu-id="8c00b-185">在 hello**簽發者**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="8c00b-185">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="8c00b-186">d.</span><span class="sxs-lookup"><span data-stu-id="8c00b-186">d.</span></span> <span data-ttu-id="8c00b-187">在 hello**驗證要求 URL**文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="8c00b-187">In hello **Authn Request URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="8c00b-188">e.</span><span class="sxs-lookup"><span data-stu-id="8c00b-188">e.</span></span> <span data-ttu-id="8c00b-189">在記事本中，複製到剪貼簿，其內容的 hello 中開啟 base-64 編碼的憑證，然後貼上 hello 整個憑證**X.509 憑證**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="8c00b-189">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste hello entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="8c00b-190">f.</span><span class="sxs-lookup"><span data-stu-id="8c00b-190">f.</span></span> <span data-ttu-id="8c00b-191">在 [電子郵件屬性] 選取 [使用 SAML 主體]。</span><span class="sxs-lookup"><span data-stu-id="8c00b-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="8c00b-192">g.</span><span class="sxs-lookup"><span data-stu-id="8c00b-192">g.</span></span> <span data-ttu-id="8c00b-193">選取 [服務提供者起始登入組態] 。</span><span class="sxs-lookup"><span data-stu-id="8c00b-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="8c00b-194">h.</span><span class="sxs-lookup"><span data-stu-id="8c00b-194">h.</span></span> <span data-ttu-id="8c00b-195">在 hello**登入路徑**文字方塊中，輸入**Azure**按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-195">In hello **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8c00b-196">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="8c00b-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8c00b-197">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="8c00b-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8c00b-198">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8c00b-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8c00b-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8c00b-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="8c00b-200">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="8c00b-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="8c00b-202">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8c00b-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c00b-203">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="8c00b-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8c00b-205">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8c00b-207">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="8c00b-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8c00b-209">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8c00b-211">a.</span><span class="sxs-lookup"><span data-stu-id="8c00b-211">a.</span></span> <span data-ttu-id="8c00b-212">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8c00b-213">b.</span><span class="sxs-lookup"><span data-stu-id="8c00b-213">b.</span></span> <span data-ttu-id="8c00b-214">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="8c00b-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8c00b-215">c.</span><span class="sxs-lookup"><span data-stu-id="8c00b-215">c.</span></span> <span data-ttu-id="8c00b-216">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8c00b-217">d.</span><span class="sxs-lookup"><span data-stu-id="8c00b-217">d.</span></span> <span data-ttu-id="8c00b-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8c00b-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="8c00b-219">建立 SumoLogic 測試使用者</span><span class="sxs-lookup"><span data-stu-id="8c00b-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="8c00b-220">在順序 tooenable Azure AD 使用者 toolog tooSumoLogic 中，它們必須已佈建的 tooSumoLogic。</span><span class="sxs-lookup"><span data-stu-id="8c00b-220">In order tooenable Azure AD users toolog in tooSumoLogic, they must be provisioned tooSumoLogic.</span></span>  

* <span data-ttu-id="8c00b-221">在 SumoLogic 的 hello 案例中，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="8c00b-221">In hello case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="8c00b-222">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8c00b-222">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c00b-223">登入 tooyour **SumoLogic**租用戶。</span><span class="sxs-lookup"><span data-stu-id="8c00b-223">Log in tooyour **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="8c00b-224">跳過**管理\>使用者**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-224">Go too**Manage \> Users**.</span></span>
   
    <span data-ttu-id="8c00b-225">![使用者](./media/active-directory-saas-sumologic-tutorial/ic778561.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="8c00b-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="8c00b-226">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="8c00b-226">Click **Add**.</span></span>
   
    <span data-ttu-id="8c00b-227">![使用者](./media/active-directory-saas-sumologic-tutorial/ic778562.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="8c00b-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="8c00b-228">在 [hello**新使用者**] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="8c00b-228">On hello **New User** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="8c00b-229">![新增使用者](./media/active-directory-saas-sumologic-tutorial/ic778563.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="8c00b-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="8c00b-230">a.</span><span class="sxs-lookup"><span data-stu-id="8c00b-230">a.</span></span> <span data-ttu-id="8c00b-231">型別 hello 相關想成 hello tooprovision hello Azure AD 帳戶資訊**名字**，**姓氏**，和**電子郵件**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="8c00b-231">Type hello related information of hello Azure AD account you want tooprovision into hello **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="8c00b-232">b.</span><span class="sxs-lookup"><span data-stu-id="8c00b-232">b.</span></span> <span data-ttu-id="8c00b-233">選取角色。</span><span class="sxs-lookup"><span data-stu-id="8c00b-233">Select a role.</span></span>
  
    <span data-ttu-id="8c00b-234">c.</span><span class="sxs-lookup"><span data-stu-id="8c00b-234">c.</span></span> <span data-ttu-id="8c00b-235">在 [狀態] 選取 [作用中]。</span><span class="sxs-lookup"><span data-stu-id="8c00b-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="8c00b-236">d.</span><span class="sxs-lookup"><span data-stu-id="8c00b-236">d.</span></span> <span data-ttu-id="8c00b-237">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8c00b-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="8c00b-238">您可以使用任何其他 SumoLogic 使用者帳戶建立工具或 Api 提供 SumoLogic tooprovision AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="8c00b-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8c00b-239">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="8c00b-239">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8c00b-240">在本節中，您可以授與存取 tooSumoLogic 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="8c00b-240">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSumoLogic.</span></span>

![指派使用者][200] 

<span data-ttu-id="8c00b-242">**tooassign 許 Simon tooSumoLogic，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="8c00b-242">**tooassign Britta Simon tooSumoLogic, perform hello following steps:**</span></span>

1. <span data-ttu-id="8c00b-243">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-243">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="8c00b-245">在 [hello] 應用程式清單中，選取**SumoLogic**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-245">In hello applications list, select **SumoLogic**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="8c00b-247">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="8c00b-247">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="8c00b-249">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8c00b-249">Click **Add** button.</span></span> <span data-ttu-id="8c00b-250">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="8c00b-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="8c00b-252">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="8c00b-252">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8c00b-253">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8c00b-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8c00b-254">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8c00b-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8c00b-255">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="8c00b-255">Testing single sign-on</span></span>

<span data-ttu-id="8c00b-256">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="8c00b-256">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8c00b-257">當您按一下 hello SumoLogic 磚 hello 存取面板中的時，您應該取得自動登入 tooyour SumoLogic 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8c00b-257">When you click hello SumoLogic tile in hello Access Panel, you should get automatically signed-on tooyour SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8c00b-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="8c00b-258">Additional resources</span></span>

* [<span data-ttu-id="8c00b-259">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c00b-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8c00b-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="8c00b-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

