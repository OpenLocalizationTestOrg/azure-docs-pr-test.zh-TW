---
title: "教學課程：Azure Active Directory 與 EthicsPoint Incident Management (EPIM) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 EthicsPoint 事件管理 」 (EPIM) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 73ef5fab815cddb3728f4b23173f99e62aec5bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="fc0b3-103">教學課程：Azure Active Directory 與 EthicsPoint Incident Management (EPIM) 整合</span><span class="sxs-lookup"><span data-stu-id="fc0b3-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="fc0b3-104">在此教學課程中，您學會如何 toointegrate EthicsPoint 事件管理 (EPIM) 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-104">In this tutorial, you learn how toointegrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc0b3-105">與 Azure AD 整合 EthicsPoint 事件管理 」 (EPIM) 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="fc0b3-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="fc0b3-106">您可以控制存取 tooEthicsPoint 事件管理 (EPIM) 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="fc0b3-106">You can control in Azure AD who has access tooEthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="fc0b3-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooEthicsPoint 事件管理 (EPIM) （單一登入）</span><span class="sxs-lookup"><span data-stu-id="fc0b3-107">You can enable your users tooautomatically get signed-on tooEthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc0b3-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fc0b3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="fc0b3-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc0b3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="fc0b3-110">Prerequisites</span></span>

<span data-ttu-id="fc0b3-111">tooconfigure Azure AD 整合與 EthicsPoint 事件管理 (EPIM)，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="fc0b3-111">tooconfigure Azure AD integration with EthicsPoint Incident Management (EPIM), you need hello following items:</span></span>

- <span data-ttu-id="fc0b3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fc0b3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc0b3-113">已啟用 EthicsPoint Incident Management (EPIM) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="fc0b3-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc0b3-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc0b3-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="fc0b3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc0b3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc0b3-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc0b3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="fc0b3-118">Scenario description</span></span>
<span data-ttu-id="fc0b3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc0b3-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="fc0b3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc0b3-121">從 hello 圖庫加入 EthicsPoint 事件管理 」 (EPIM)</span><span class="sxs-lookup"><span data-stu-id="fc0b3-121">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
2. <span data-ttu-id="fc0b3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fc0b3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-hello-gallery"></a><span data-ttu-id="fc0b3-123">從 hello 圖庫加入 EthicsPoint 事件管理 」 (EPIM)</span><span class="sxs-lookup"><span data-stu-id="fc0b3-123">Adding EthicsPoint Incident Management (EPIM) from hello gallery</span></span>
<span data-ttu-id="fc0b3-124">tooconfigure hello 整合 EthicsPoint 事件管理 」 (EPIM) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd EthicsPoint 事件管理 」 (EPIM)。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-124">tooconfigure hello integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need tooadd EthicsPoint Incident Management (EPIM) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="fc0b3-125">**tooadd EthicsPoint 事件管理 (EPIM) 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fc0b3-125">**tooadd EthicsPoint Incident Management (EPIM) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc0b3-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc0b3-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="fc0b3-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="fc0b3-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="fc0b3-133">在 [hello] 搜尋方塊中，輸入**EthicsPoint 事件管理 」 (EPIM)**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-133">In hello search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="fc0b3-135">在 hello 結果 窗格中，選取  **EthicsPoint 事件管理 」 (EPIM)**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-135">In hello results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc0b3-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fc0b3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fc0b3-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 EthicsPoint Incident Management (EPIM) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fc0b3-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 EthicsPoint 事件管理 (EPIM) 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in EthicsPoint Incident Management (EPIM) is tooa user in Azure AD.</span></span> <span data-ttu-id="fc0b3-140">換句話說，Azure AD 使用者與 hello 相關的使用者 EthicsPoint 事件管理 (EPIM) 之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-140">In other words, a link relationship between an Azure AD user and hello related user in EthicsPoint Incident Management (EPIM) needs toobe established.</span></span>

<span data-ttu-id="fc0b3-141">在 EthicsPoint 事件管理 (EPIM) 中，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-141">In EthicsPoint Incident Management (EPIM), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="fc0b3-142">tooconfigure 及 EthicsPoint 事件管理 (EPIM) 與 Azure AD 單一登入測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="fc0b3-142">tooconfigure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="fc0b3-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="fc0b3-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc0b3-145">**[建立 EthicsPoint 事件管理 」 (EPIM) 測試使用者](#creating-a-ethicspoint-incident-management-epim-test-user)** -toohave 許 Simon 中 EthicsPoint 事件管理 (EPIM) 表示法連結的 toohello Azure AD 使用者的對應項目。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - toohave a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc0b3-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc0b3-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc0b3-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="fc0b3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc0b3-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 EthicsPoint 事件管理 」 (EPIM) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="fc0b3-150">**tooconfigure Azure AD 單一登入與 EthicsPoint 事件管理 (EPIM) 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fc0b3-150">**tooconfigure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="fc0b3-151">在 Azure 入口網站上 hello hello **EthicsPoint 事件管理 」 (EPIM)**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-151">In hello Azure portal, on hello **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="fc0b3-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="fc0b3-155">在 hello **EthicsPoint 事件管理 」 (EPIM) 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc0b3-155">On hello **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="fc0b3-157">a.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-157">a.</span></span> <span data-ttu-id="fc0b3-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc0b3-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="fc0b3-159">b.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-159">b.</span></span> <span data-ttu-id="fc0b3-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="fc0b3-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="fc0b3-161">c.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-161">c.</span></span> <span data-ttu-id="fc0b3-162">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<servername>.navexglobal.com/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="fc0b3-162">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc0b3-163">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-163">These values are not real.</span></span> <span data-ttu-id="fc0b3-164">更新這些值與 hello 實際的回覆 URL、 識別碼和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-164">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="fc0b3-165">請連絡[EthicsPoint 事件管理 」 (EPIM) 用戶端支援小組](http://www.navexglobal.com/company/contact-us)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) tooget these values.</span></span> 

4. <span data-ttu-id="fc0b3-166">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="fc0b3-168">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-168">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="fc0b3-170">tooconfigure 單一登入上**EthicsPoint 事件管理 」 (EPIM)**端，您需要下載 toosend hello**中繼資料 XML**太[EthicsPoint 事件管理 」 (EPIM) 支援小組](http://www.navexglobal.com/company/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-170">tooconfigure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need toosend hello downloaded **Metadata XML** too[EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="fc0b3-171">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="fc0b3-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="fc0b3-172">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="fc0b3-173">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="fc0b3-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc0b3-174">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fc0b3-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc0b3-175">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="fc0b3-177">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fc0b3-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="fc0b3-178">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc0b3-180">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc0b3-182">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc0b3-184">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="fc0b3-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc0b3-186">a.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-186">a.</span></span> <span data-ttu-id="fc0b3-187">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc0b3-188">b.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-188">b.</span></span> <span data-ttu-id="fc0b3-189">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc0b3-190">c.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-190">c.</span></span> <span data-ttu-id="fc0b3-191">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="fc0b3-192">d.</span><span class="sxs-lookup"><span data-stu-id="fc0b3-192">d.</span></span> <span data-ttu-id="fc0b3-193">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="fc0b3-194">建立 EthicsPoint Incident Management (EPIM) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="fc0b3-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="fc0b3-195">在本節中，您要在 EthicsPoint Incident Management (EPIM) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="fc0b3-196">請使用[EthicsPoint 事件管理 」 (EPIM) 支援小組](http://www.navexglobal.com/company/contact-us)tooadd hello hello EthicsPoint 事件管理 」 (EPIM) 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) tooadd hello users in hello EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="fc0b3-197">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="fc0b3-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="fc0b3-198">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooEthicsPoint 事件管理 (EPIM)。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEthicsPoint Incident Management (EPIM).</span></span>

![指派使用者][200] 

<span data-ttu-id="fc0b3-200">**tooassign 許 Simon tooEthicsPoint 事件管理 (EPIM)，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="fc0b3-200">**tooassign Britta Simon tooEthicsPoint Incident Management (EPIM), perform hello following steps:**</span></span>

1. <span data-ttu-id="fc0b3-201">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="fc0b3-203">在 [hello] 應用程式清單中，選取**EthicsPoint 事件管理 」 (EPIM)**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-203">In hello applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="fc0b3-205">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="fc0b3-207">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-207">Click **Add** button.</span></span> <span data-ttu-id="fc0b3-208">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="fc0b3-210">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="fc0b3-211">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc0b3-212">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc0b3-213">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="fc0b3-213">Testing single sign-on</span></span>

<span data-ttu-id="fc0b3-214">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="fc0b3-215">當您按一下 hello EthicsPoint 事件管理 」 (EPIM) 磚 hello 存取面板中的時，您應該取得自動登入 tooyour EthicsPoint 事件管理 」 (EPIM) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="fc0b3-215">When you click hello EthicsPoint Incident Management (EPIM) tile in hello Access Panel, you should get automatically signed-on tooyour EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fc0b3-216">其他資源</span><span class="sxs-lookup"><span data-stu-id="fc0b3-216">Additional resources</span></span>

* [<span data-ttu-id="fc0b3-217">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc0b3-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc0b3-218">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="fc0b3-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

