---
title: "教學課程：Azure Active Directory 與 TOPdesk - Public 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 TOPdesk-Public 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="5d602-103">教學課程：Azure Active Directory 與 TOPdesk - Public 整合</span><span class="sxs-lookup"><span data-stu-id="5d602-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="5d602-104">在此教學課程中，您學會如何 toointegrate TOPdesk-Public 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="5d602-104">In this tutorial, you learn how toointegrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5d602-105">整合 TOPdesk-Public 與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-105">Integrating TOPdesk - Public with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5d602-106">您可以控制存取 tooTOPdesk-Public 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5d602-106">You can control in Azure AD who has access tooTOPdesk - Public.</span></span>
- <span data-ttu-id="5d602-107">您可以啟用您的使用者 tooautomatically get 登入 tooTOPdesk-公用 （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d602-107">You can enable your users tooautomatically get signed-on tooTOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5d602-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="5d602-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5d602-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="5d602-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d602-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="5d602-110">Prerequisites</span></span>

<span data-ttu-id="5d602-111">tooconfigure Azure AD 整合與 TOPdesk-Public，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-111">tooconfigure Azure AD integration with TOPdesk - Public, you need hello following items:</span></span>

- <span data-ttu-id="5d602-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d602-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5d602-113">已啟用 TOPdesk - Public 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="5d602-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5d602-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="5d602-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5d602-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="5d602-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5d602-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="5d602-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5d602-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5d602-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5d602-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="5d602-118">Scenario description</span></span>
<span data-ttu-id="5d602-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5d602-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5d602-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="5d602-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5d602-121">加入 TOPdesk-Public 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="5d602-121">Adding TOPdesk - Public from hello gallery</span></span>
2. <span data-ttu-id="5d602-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5d602-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-hello-gallery"></a><span data-ttu-id="5d602-123">加入 TOPdesk-Public 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="5d602-123">Adding TOPdesk - Public from hello gallery</span></span>
<span data-ttu-id="5d602-124">tooconfigure hello 整合 TOPdesk-Public 到 Azure AD，您需要 tooadd TOPdesk-Public hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d602-124">tooconfigure hello integration of TOPdesk - Public into Azure AD, you need tooadd TOPdesk - Public from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5d602-125">**tooadd TOPdesk-Public hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5d602-125">**tooadd TOPdesk - Public from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d602-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="5d602-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="5d602-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5d602-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5d602-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5d602-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="5d602-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d602-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="5d602-133">在 [hello] 搜尋方塊中，輸入**TOPdesk-Public**，選取**TOPdesk-Public**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d602-133">In hello search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button tooadd hello application.</span></span>

    ![TOPdesk-Public hello [結果] 清單中](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5d602-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5d602-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5d602-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 TOPdesk - Public 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5d602-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5d602-137">針對單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者在 [TOPdesk-Public tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="5d602-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in TOPdesk - Public is tooa user in Azure AD.</span></span> <span data-ttu-id="5d602-138">也就是說，連結之間的關聯性的 Azure AD 使用者和 hello 相關的使用者，在 [TOPdesk-Public 需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="5d602-138">In other words, a link relationship between an Azure AD user and hello related user in TOPdesk - Public needs toobe established.</span></span>

<span data-ttu-id="5d602-139">在 TOPdesk-Public、 hello 分派 hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="5d602-139">In TOPdesk - Public, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5d602-140">tooconfigure 和測試 Azure AD 單一登入與 TOPdesk-Public，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-140">tooconfigure and test Azure AD single sign-on with TOPdesk - Public, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5d602-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="5d602-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5d602-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="5d602-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5d602-143">**[建立 TOPdesk-Public 的測試使用者](#create-a-topdesk---public-test-user)** -toohave 許 Simon TOPdesk 中對應項目-是連結的 toohello Azure AD 使用者表示法的公用。</span><span class="sxs-lookup"><span data-stu-id="5d602-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - toohave a counterpart of Britta Simon in TOPdesk - Public that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5d602-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5d602-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5d602-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="5d602-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5d602-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="5d602-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5d602-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 TOPdesk-Public 的應用程式中。</span><span class="sxs-lookup"><span data-stu-id="5d602-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="5d602-148">**Azure AD 單一登入的 tooconfigure 與 TOPdesk-Public，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5d602-148">**tooconfigure Azure AD single sign-on with TOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d602-149">在 Azure 入口網站上 hello hello **TOPdesk-Public**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="5d602-149">In hello Azure portal, on hello **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="5d602-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="5d602-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="5d602-153">在 [hello **TOPdesk-公用網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-153">On hello **TOPdesk - Public Domain and URLs** section, perform hello following steps:</span></span>

    ![TOPdesk - Public 網域與 URL 單一登入資訊](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="5d602-155">a.</span><span class="sxs-lookup"><span data-stu-id="5d602-155">a.</span></span> <span data-ttu-id="5d602-156">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="5d602-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="5d602-157">b.</span><span class="sxs-lookup"><span data-stu-id="5d602-157">b.</span></span> <span data-ttu-id="5d602-158">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="5d602-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="5d602-159">c.</span><span class="sxs-lookup"><span data-stu-id="5d602-159">c.</span></span> <span data-ttu-id="5d602-160">在 [hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="5d602-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="5d602-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="5d602-161">These values are not real.</span></span> <span data-ttu-id="5d602-162">更新這些值與實際的 hello，識別項、 回覆 URL 和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="5d602-162">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5d602-163">[回覆 URL] 稍後會在本教學課程中說明。</span><span class="sxs-lookup"><span data-stu-id="5d602-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="5d602-164">請連絡[TOPdesk-Public 的用戶端支援小組](https://help.topdesk.com/saas/enterprise/user/)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="5d602-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) tooget these values.</span></span>  

4. <span data-ttu-id="5d602-165">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="5d602-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="5d602-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d602-167">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="5d602-169">在 [hello **TOPdesk-公用組態**區段中，按一下**設定 TOPdesk-Public** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="5d602-169">On hello **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5d602-170">複製 hello**登出 URL、 SAML 實體識別碼、 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="5d602-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![TOPdesk - Public 設定](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="5d602-172">登入 tooyour **TOPdesk-Public**系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="5d602-172">Sign on tooyour **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="5d602-173">在 [hello **TOPdesk**功能表上，按一下 [**設定**。</span><span class="sxs-lookup"><span data-stu-id="5d602-173">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="5d602-174">![設定](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "設定")</span><span class="sxs-lookup"><span data-stu-id="5d602-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="5d602-175">按一下 [登入設定] 。</span><span class="sxs-lookup"><span data-stu-id="5d602-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="5d602-176">![登入設定](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="5d602-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="5d602-177">展開 hello**登入設定**功能表，然後再按一下**一般**。</span><span class="sxs-lookup"><span data-stu-id="5d602-177">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="5d602-178">![一般](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "一般")</span><span class="sxs-lookup"><span data-stu-id="5d602-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="5d602-179">在 [hello**公用**區段 hello **SAML 登入**組態區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-179">In hello **Public** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5d602-180">![技術設定](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "技術設定")</span><span class="sxs-lookup"><span data-stu-id="5d602-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="5d602-181">a.</span><span class="sxs-lookup"><span data-stu-id="5d602-181">a.</span></span> <span data-ttu-id="5d602-182">按一下**下載**toodownload hello 公用中繼資料檔案，然後將它儲存在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="5d602-182">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="5d602-183">b.</span><span class="sxs-lookup"><span data-stu-id="5d602-183">b.</span></span> <span data-ttu-id="5d602-184">開啟 hello 下載中繼資料檔案，然後再找出 hello **AssertionConsumerService**節點。</span><span class="sxs-lookup"><span data-stu-id="5d602-184">Open hello downloaded metadata file, and then locate hello **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="5d602-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="5d602-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="5d602-186">c.</span><span class="sxs-lookup"><span data-stu-id="5d602-186">c.</span></span> <span data-ttu-id="5d602-187">複製 hello **AssertionConsumerService**值，請將此值貼入中 hello**回覆 URL** ] 文字方塊中的**TOPdesk-公用網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="5d602-187">Copy hello **AssertionConsumerService** value, paste this value in hello **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="5d602-188">toocreate 憑證檔案，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-188">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="5d602-189">![憑證](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "憑證")</span><span class="sxs-lookup"><span data-stu-id="5d602-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="5d602-190">a.</span><span class="sxs-lookup"><span data-stu-id="5d602-190">a.</span></span> <span data-ttu-id="5d602-191">開啟 hello 從 Azure 入口網站下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="5d602-191">Open hello downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="5d602-192">b.</span><span class="sxs-lookup"><span data-stu-id="5d602-192">b.</span></span> <span data-ttu-id="5d602-193">展開 hello **RoleDescriptor**節點具有**xsi: type**的**fed: ApplicationServiceType**。</span><span class="sxs-lookup"><span data-stu-id="5d602-193">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="5d602-194">c.</span><span class="sxs-lookup"><span data-stu-id="5d602-194">c.</span></span> <span data-ttu-id="5d602-195">複製 hello hello 值**X509Certificate**節點。</span><span class="sxs-lookup"><span data-stu-id="5d602-195">Copy hello value of hello **X509Certificate** node.</span></span>
    
    <span data-ttu-id="5d602-196">d.</span><span class="sxs-lookup"><span data-stu-id="5d602-196">d.</span></span> <span data-ttu-id="5d602-197">複製儲存 hello **X509Certificate**在檔案中的電腦上本機值。</span><span class="sxs-lookup"><span data-stu-id="5d602-197">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="5d602-198">在 [hello**公用**區段中，按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="5d602-198">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="5d602-199">![SAML 登入](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML 登入")</span><span class="sxs-lookup"><span data-stu-id="5d602-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="5d602-200">在 [hello **SAML 設定助理**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-200">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="5d602-201">![SAML 組態輔助程式](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML 組態輔助程式")</span><span class="sxs-lookup"><span data-stu-id="5d602-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="5d602-202">a.</span><span class="sxs-lookup"><span data-stu-id="5d602-202">a.</span></span> <span data-ttu-id="5d602-203">tooupload 下載的中繼資料檔案從 Azure 入口網站底下**同盟中繼資料**，按一下 [**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="5d602-203">tooupload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="5d602-204">b.</span><span class="sxs-lookup"><span data-stu-id="5d602-204">b.</span></span> <span data-ttu-id="5d602-205">在您的憑證檔案的 tooupload**憑證 (RSA)**，按一下 [**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="5d602-205">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="5d602-206">c.</span><span class="sxs-lookup"><span data-stu-id="5d602-206">c.</span></span> <span data-ttu-id="5d602-207">所得 hello TOPdesk 支援小組，底下 tooupload hello 標誌檔**標誌圖示**，按一下 [**瀏覽**。</span><span class="sxs-lookup"><span data-stu-id="5d602-207">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="5d602-208">d.</span><span class="sxs-lookup"><span data-stu-id="5d602-208">d.</span></span> <span data-ttu-id="5d602-209">在 [hello**使用者名稱屬性**文字方塊中，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="5d602-209">In hello **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="5d602-210">e.</span><span class="sxs-lookup"><span data-stu-id="5d602-210">e.</span></span> <span data-ttu-id="5d602-211">在 [hello**顯示名稱**文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="5d602-211">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="5d602-212">f.</span><span class="sxs-lookup"><span data-stu-id="5d602-212">f.</span></span> <span data-ttu-id="5d602-213">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5d602-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5d602-214">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="5d602-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5d602-215">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="5d602-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5d602-216">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5d602-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5d602-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5d602-217">Create an Azure AD test user</span></span>

<span data-ttu-id="5d602-218">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="5d602-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="5d602-220">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5d602-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d602-221">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d602-221">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5d602-223">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="5d602-223">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5d602-225">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="5d602-225">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5d602-227">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-227">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5d602-229">a.</span><span class="sxs-lookup"><span data-stu-id="5d602-229">a.</span></span> <span data-ttu-id="5d602-230">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="5d602-230">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5d602-231">b.</span><span class="sxs-lookup"><span data-stu-id="5d602-231">b.</span></span> <span data-ttu-id="5d602-232">在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="5d602-232">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5d602-233">c.</span><span class="sxs-lookup"><span data-stu-id="5d602-233">c.</span></span> <span data-ttu-id="5d602-234">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="5d602-234">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5d602-235">d.</span><span class="sxs-lookup"><span data-stu-id="5d602-235">d.</span></span> <span data-ttu-id="5d602-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="5d602-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="5d602-237">建立 TOPdesk-Public 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5d602-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="5d602-238">在訂單 tooenable Azure AD 使用者 toolog 到 TOPdesk-Public，您必須佈建到 TOPdesk-Public。</span><span class="sxs-lookup"><span data-stu-id="5d602-238">In order tooenable Azure AD users toolog into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="5d602-239">Hello 案例 TOPdesk-Public，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="5d602-239">In hello case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="5d602-240">tooconfigure 使用者佈建，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-240">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="5d602-241">登入 tooyour **TOPdesk-Public**以系統管理員身分的公司網站。</span><span class="sxs-lookup"><span data-stu-id="5d602-241">Sign on tooyour **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="5d602-242">在 [hello 最上層顯示 hello 功能表上，按一下**TOPdesk\>新增\>支援檔案\>人員**。</span><span class="sxs-lookup"><span data-stu-id="5d602-242">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="5d602-243">![人員](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "人員")</span><span class="sxs-lookup"><span data-stu-id="5d602-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="5d602-244">在 hello 新增人員] 對話方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="5d602-244">On hello New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5d602-245">![新增人員](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "新增人員")</span><span class="sxs-lookup"><span data-stu-id="5d602-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="5d602-246">a.</span><span class="sxs-lookup"><span data-stu-id="5d602-246">a.</span></span> <span data-ttu-id="5d602-247">按一下 hello 一般索引標籤。</span><span class="sxs-lookup"><span data-stu-id="5d602-247">Click hello General tab.</span></span>

    <span data-ttu-id="5d602-248">b.</span><span class="sxs-lookup"><span data-stu-id="5d602-248">b.</span></span> <span data-ttu-id="5d602-249">在 [hello**姓氏**文字方塊中，輸入像 Simon hello 使用者的姓氏</span><span class="sxs-lookup"><span data-stu-id="5d602-249">In hello **Surname** textbox, type Surname of hello user like Simon</span></span>
 
    <span data-ttu-id="5d602-250">c.</span><span class="sxs-lookup"><span data-stu-id="5d602-250">c.</span></span> <span data-ttu-id="5d602-251">選取**網站**hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d602-251">Select a **Site** for hello account.</span></span>
 
    <span data-ttu-id="5d602-252">d.</span><span class="sxs-lookup"><span data-stu-id="5d602-252">d.</span></span> <span data-ttu-id="5d602-253">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="5d602-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="5d602-254">您可以使用任何其他 TOPdesk-Public 使用者帳戶建立工具或 Api TOPdesk-Public tooprovision Azure AD 使用者帳戶所提供。</span><span class="sxs-lookup"><span data-stu-id="5d602-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5d602-255">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="5d602-255">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5d602-256">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooTOPdesk-Public。</span><span class="sxs-lookup"><span data-stu-id="5d602-256">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTOPdesk - Public.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="5d602-258">**tooassign 許 Simon tooTOPdesk-公用的執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="5d602-258">**tooassign Britta Simon tooTOPdesk - Public, perform hello following steps:**</span></span>

1. <span data-ttu-id="5d602-259">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="5d602-259">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="5d602-261">在 [hello] 應用程式清單中，選取**TOPdesk-Public**。</span><span class="sxs-lookup"><span data-stu-id="5d602-261">In hello applications list, select **TOPdesk - Public**.</span></span>

    ![hello 應用程式清單中的 hello TOPdesk-Public 連結](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="5d602-263">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="5d602-263">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="5d602-265">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d602-265">Click **Add** button.</span></span> <span data-ttu-id="5d602-266">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="5d602-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="5d602-268">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="5d602-268">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5d602-269">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d602-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5d602-270">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5d602-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5d602-271">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="5d602-271">Test single sign-on</span></span>

<span data-ttu-id="5d602-272">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="5d602-272">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5d602-273">當您按一下 hello TOPdesk-Public 磚 hello 存取面板中，您應該取得自動登入 tooyour TOPdesk-Public 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="5d602-273">When you click hello TOPdesk - Public tile in hello Access Panel, you should get automatically signed-on tooyour TOPdesk - Public application.</span></span>
<span data-ttu-id="5d602-274">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="5d602-274">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5d602-275">其他資源</span><span class="sxs-lookup"><span data-stu-id="5d602-275">Additional resources</span></span>

* [<span data-ttu-id="5d602-276">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d602-276">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5d602-277">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="5d602-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

