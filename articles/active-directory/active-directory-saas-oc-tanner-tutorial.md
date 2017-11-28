---
title: "教學課程：Azure Active Directory 與 O.C.  Tanner - AppreciateHub 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 O.C.之間 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 45052cf56e35746d7df5910162e40e3bbcad1aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="31340-105">教學課程：Azure Active Directory 與 O.C. </span><span class="sxs-lookup"><span data-stu-id="31340-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="31340-106">Tanner - AppreciateHub 的人員</span><span class="sxs-lookup"><span data-stu-id="31340-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="31340-107">在此教學課程中，您學會如何 toointegrate O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-107">In this tutorial, you learn how toointegrate O.C.</span></span> <span data-ttu-id="31340-108">Tanner - AppreciateHub 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="31340-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="31340-109">整合 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-109">Integrating O.C.</span></span> <span data-ttu-id="31340-110">Tanner-AppreciateHub 與 Azure AD 提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="31340-110">Tanner - AppreciateHub with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="31340-111">您可以控制存取 tooO.C Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="31340-111">You can control in Azure AD who has access tooO.C.</span></span> <span data-ttu-id="31340-112">Tanner - AppreciateHub 的人員</span><span class="sxs-lookup"><span data-stu-id="31340-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="31340-113">您可以啟用您的使用者 tooautomatically get 登入 tooO.C。</span><span class="sxs-lookup"><span data-stu-id="31340-113">You can enable your users tooautomatically get signed-on tooO.C.</span></span> <span data-ttu-id="31340-114">Tanner - AppreciateHub (單一登入)</span><span class="sxs-lookup"><span data-stu-id="31340-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="31340-115">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="31340-115">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="31340-116">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="31340-116">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31340-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="31340-117">Prerequisites</span></span>

<span data-ttu-id="31340-118">tooconfigure O.C.與 Azure AD 整合</span><span class="sxs-lookup"><span data-stu-id="31340-118">tooconfigure Azure AD integration with O.C.</span></span> <span data-ttu-id="31340-119">Tanner-AppreciateHub，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="31340-119">Tanner - AppreciateHub, you need hello following items:</span></span>

- <span data-ttu-id="31340-120">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="31340-120">An Azure AD subscription</span></span>
- <span data-ttu-id="31340-121">啟用 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-121">A O.C.</span></span> <span data-ttu-id="31340-122">Tanner - AppreciateHub 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="31340-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="31340-123">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="31340-123">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="31340-124">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="31340-124">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="31340-125">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="31340-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="31340-126">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="31340-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="31340-127">案例描述</span><span class="sxs-lookup"><span data-stu-id="31340-127">Scenario description</span></span>
<span data-ttu-id="31340-128">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31340-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="31340-129">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="31340-129">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="31340-130">從組件庫新增 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-130">Adding O.C.</span></span> <span data-ttu-id="31340-131">Tanner-AppreciateHub 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="31340-131">Tanner - AppreciateHub from hello gallery</span></span>
2. <span data-ttu-id="31340-132">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31340-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-hello-gallery"></a><span data-ttu-id="31340-133">從組件庫新增 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-133">Adding O.C.</span></span> <span data-ttu-id="31340-134">Tanner-AppreciateHub 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="31340-134">Tanner - AppreciateHub from hello gallery</span></span>
<span data-ttu-id="31340-135">tooconfigure hello 整合的 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-135">tooconfigure hello integration of O.C.</span></span> <span data-ttu-id="31340-136">Tanner-AppreciateHub 到 Azure AD，您需要 tooadd O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-136">Tanner - AppreciateHub into Azure AD, you need tooadd O.C.</span></span> <span data-ttu-id="31340-137">Tanner-AppreciateHub hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31340-137">Tanner - AppreciateHub from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="31340-138">**tooadd O.C.Tanner-AppreciateHub 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="31340-138">**tooadd O.C. Tanner - AppreciateHub from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="31340-139">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="31340-139">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="31340-141">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="31340-141">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="31340-142">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="31340-142">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="31340-144">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="31340-144">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="31340-146">在 [hello] 搜尋方塊中，輸入**O.C.Tanner - AppreciateHub**。</span><span class="sxs-lookup"><span data-stu-id="31340-146">In hello search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="31340-148">在 hello 結果 窗格中，選取  **O.C.Tanner-AppreciateHub**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31340-148">In hello results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="31340-150">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31340-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="31340-151">在本節中，您會設定及測試與 O.C. 搭配運作的 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31340-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="31340-152">Tanner - AppreciateHub。</span><span class="sxs-lookup"><span data-stu-id="31340-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="31340-153">單一登入 toowork，Azure AD 需要 tooknow O.C.中的 hello 對等項目的使用者</span><span class="sxs-lookup"><span data-stu-id="31340-153">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in O.C.</span></span> <span data-ttu-id="31340-154">Tanner-AppreciateHub 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="31340-154">Tanner - AppreciateHub is tooa user in Azure AD.</span></span> <span data-ttu-id="31340-155">換句話說，Azure AD 使用者和 hello O.C.中相關的使用者之間的連結關聯性</span><span class="sxs-lookup"><span data-stu-id="31340-155">In other words, a link relationship between an Azure AD user and hello related user in O.C.</span></span> <span data-ttu-id="31340-156">Tanner-AppreciateHub 需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="31340-156">Tanner - AppreciateHub needs toobe established.</span></span>

<span data-ttu-id="31340-157">在 O.C. </span><span class="sxs-lookup"><span data-stu-id="31340-157">In O.C.</span></span> <span data-ttu-id="31340-158">Hello Tanner-AppreciateHub，指派 hello 值**使用者名**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="31340-158">Tanner - AppreciateHub, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="31340-159">tooconfigure 和測試 Azure AD 單一登入與 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-159">tooconfigure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="31340-160">Tanner-AppreciateHub，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="31340-160">Tanner - AppreciateHub, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="31340-161">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="31340-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="31340-162">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="31340-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="31340-163">**[建立 O.C.Tanner-AppreciateHub 測試使用者](#creating-a-oc-tanner---appreciatehub-test-user)** -toohave 許 Simon O.C.中對應項目</span><span class="sxs-lookup"><span data-stu-id="31340-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - toohave a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="31340-164">Tanner-AppreciateHub 所連結的 toohello Azure AD 使用者表示法。</span><span class="sxs-lookup"><span data-stu-id="31340-164">Tanner - AppreciateHub that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="31340-165">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31340-165">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="31340-166">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="31340-166">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="31340-167">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="31340-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="31340-168">在本節中，方法，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入您 O.C.中</span><span class="sxs-lookup"><span data-stu-id="31340-168">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="31340-169">Tanner - AppreciateHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31340-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="31340-170">**tooconfigure Azure AD 單一登入與 O.C.Tanner-AppreciateHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="31340-170">**tooconfigure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="31340-171">在 Azure 入口網站上 hello hello **O.C.Tanner-AppreciateHub**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="31340-171">In hello Azure portal, on hello **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="31340-173">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31340-173">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="31340-175">在 hello **O.C.Tanner-AppreciateHub 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="31340-175">On hello **O.C. Tanner - AppreciateHub Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="31340-177">a.</span><span class="sxs-lookup"><span data-stu-id="31340-177">a.</span></span> <span data-ttu-id="31340-178">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="31340-178">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="31340-179">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="31340-179">This value is not real.</span></span> <span data-ttu-id="31340-180">更新此值與 hello 實際的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="31340-180">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="31340-181">請連絡[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="31340-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) tooget this value.</span></span>

    <span data-ttu-id="31340-182">b.</span><span class="sxs-lookup"><span data-stu-id="31340-182">b.</span></span> <span data-ttu-id="31340-183">使用下列連結的 hello 開啟 hello 中繼資料檔案： [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata)。</span><span class="sxs-lookup"><span data-stu-id="31340-183">Open hello metadata file using hello following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="31340-184">c.</span><span class="sxs-lookup"><span data-stu-id="31340-184">c.</span></span> <span data-ttu-id="31340-185">找出 hello **md:AssertionConsumerService**節點。</span><span class="sxs-lookup"><span data-stu-id="31340-185">Locate hello **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="31340-186">d.</span><span class="sxs-lookup"><span data-stu-id="31340-186">d.</span></span> <span data-ttu-id="31340-187">複製 hello hello 值**位置**屬性。</span><span class="sxs-lookup"><span data-stu-id="31340-187">Copy hello value of hello **Location** attribute.</span></span> 
   
    ![設定 App 設定][12]
   
    <span data-ttu-id="31340-189">e.</span><span class="sxs-lookup"><span data-stu-id="31340-189">e.</span></span> <span data-ttu-id="31340-190">在 hello**登入 URL**文字方塊中，超過 hello hello 上一個步驟中取得的值。</span><span class="sxs-lookup"><span data-stu-id="31340-190">In hello **Sign On URL** textbox, past hello value you have obtained in hello previous step.</span></span>

4. <span data-ttu-id="31340-191">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="31340-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="31340-193">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="31340-193">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="31340-195">tooconfigure 單一登入上**O.C.Tanner-AppreciateHub**端，您需要下載 toosend hello**中繼資料 XML**太[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)。</span><span class="sxs-lookup"><span data-stu-id="31340-195">tooconfigure single sign-on on **O.C. Tanner - AppreciateHub** side, you need toosend hello downloaded **Metadata XML** too[O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="31340-196">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="31340-196">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="31340-197">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="31340-197">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="31340-198">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="31340-198">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="31340-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31340-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="31340-200">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="31340-200">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="31340-202">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="31340-202">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="31340-203">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="31340-203">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="31340-205">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="31340-205">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="31340-207">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="31340-207">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="31340-209">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="31340-209">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="31340-211">a.</span><span class="sxs-lookup"><span data-stu-id="31340-211">a.</span></span> <span data-ttu-id="31340-212">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="31340-212">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="31340-213">b.</span><span class="sxs-lookup"><span data-stu-id="31340-213">b.</span></span> <span data-ttu-id="31340-214">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="31340-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="31340-215">c.</span><span class="sxs-lookup"><span data-stu-id="31340-215">c.</span></span> <span data-ttu-id="31340-216">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="31340-216">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="31340-217">d.</span><span class="sxs-lookup"><span data-stu-id="31340-217">d.</span></span> <span data-ttu-id="31340-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="31340-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="31340-219">建立 O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-219">Creating a O.C.</span></span> <span data-ttu-id="31340-220">Tanner - AppreciateHub 測試使用者</span><span class="sxs-lookup"><span data-stu-id="31340-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="31340-221">hello 本節目標在於 toocreate O.C.中呼叫許 Simon 的使用者</span><span class="sxs-lookup"><span data-stu-id="31340-221">hello objective of this section is toocreate a user called Britta Simon in O.C.</span></span> <span data-ttu-id="31340-222">Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="31340-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="31340-223">**toocreate 使用者呼叫許 Simon O.C.Tanner-AppreciateHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="31340-223">**toocreate a user called Britta Simon in O.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

<span data-ttu-id="31340-224">請要求您[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)toocreate 具有做為 nameID 屬性 hello 相同的值為 hello 使用者名稱，Simon 許在 Azure AD 中的使用者。</span><span class="sxs-lookup"><span data-stu-id="31340-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) toocreate a user that has as nameID attribute hello same value as hello user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="31340-225">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="31340-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="31340-226">在本節中，您可以授與存取 tooO.C 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="31340-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooO.C.</span></span> <span data-ttu-id="31340-227">Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="31340-227">Tanner - AppreciateHub.</span></span>

![指派使用者][200] 

<span data-ttu-id="31340-229">**tooassign 許 Simon tooO.C。Tanner-AppreciateHub，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="31340-229">**tooassign Britta Simon tooO.C. Tanner - AppreciateHub, perform hello following steps:**</span></span>

1. <span data-ttu-id="31340-230">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="31340-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="31340-232">在 [hello] 應用程式清單中，選取**O.C.Tanner - AppreciateHub**。</span><span class="sxs-lookup"><span data-stu-id="31340-232">In hello applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="31340-234">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="31340-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="31340-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31340-236">Click **Add** button.</span></span> <span data-ttu-id="31340-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="31340-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="31340-239">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="31340-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="31340-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31340-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="31340-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="31340-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="31340-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="31340-242">Testing single sign-on</span></span>

<span data-ttu-id="31340-243">hello 本節目標在於 tootest 您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="31340-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="31340-244">當您按一下 hello O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-244">When you click hello O.C.</span></span> <span data-ttu-id="31340-245">Tanner-AppreciateHub 磚 hello 存取面板中，您應該取得自動登入 tooyour O.C.</span><span class="sxs-lookup"><span data-stu-id="31340-245">Tanner - AppreciateHub tile in hello Access Panel, you should get automatically signed-on tooyour O.C.</span></span> <span data-ttu-id="31340-246">Tanner - AppreciateHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="31340-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="31340-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="31340-247">Additional resources</span></span>

* [<span data-ttu-id="31340-248">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="31340-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="31340-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="31340-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

