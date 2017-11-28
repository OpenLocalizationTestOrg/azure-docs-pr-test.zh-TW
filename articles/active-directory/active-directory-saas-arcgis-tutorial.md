---
title: "教學課程：Azure Active Directory 與 ArcGIS Online 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 ArcGIS Online 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: f3dd55d798cf3256fb2758e011f33946baa405ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="77e4b-103">教學課程：Azure Active Directory 與 ArcGIS Online 整合</span><span class="sxs-lookup"><span data-stu-id="77e4b-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="77e4b-104">在此教學課程中，您學會如何 toointegrate ArcGIS Online 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="77e4b-104">In this tutorial, you learn how toointegrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="77e4b-105">與 Azure AD 整合 ArcGIS 線上可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-105">Integrating ArcGIS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="77e4b-106">您可以控制存取 tooArcGIS 線上 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="77e4b-106">You can control in Azure AD who has access tooArcGIS Online</span></span>
- <span data-ttu-id="77e4b-107">您可以啟用您的使用者 tooautomatically get 登入 tooArcGIS 線上 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="77e4b-107">You can enable your users tooautomatically get signed-on tooArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="77e4b-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="77e4b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="77e4b-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="77e4b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with ArcGIS Online, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="77e4b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="77e4b-110">Prerequisites</span></span>

<span data-ttu-id="77e4b-111">tooconfigure 與線上 ArcGIS 的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-111">tooconfigure Azure AD integration with ArcGIS Online, you need hello following items:</span></span>

- <span data-ttu-id="77e4b-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77e4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="77e4b-113">已啟用 ArcGIS Online 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="77e4b-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="77e4b-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="77e4b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="77e4b-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="77e4b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="77e4b-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="77e4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="77e4b-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="77e4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="77e4b-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="77e4b-118">Scenario description</span></span>
<span data-ttu-id="77e4b-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77e4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="77e4b-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="77e4b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="77e4b-121">新增線上 ArcGIS 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="77e4b-121">Adding ArcGIS Online from hello gallery</span></span>
2. <span data-ttu-id="77e4b-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77e4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-hello-gallery"></a><span data-ttu-id="77e4b-123">新增線上 ArcGIS 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="77e4b-123">Adding ArcGIS Online from hello gallery</span></span>
<span data-ttu-id="77e4b-124">tooconfigure hello 整合 ArcGIS 線上到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd ArcGIS 線上。</span><span class="sxs-lookup"><span data-stu-id="77e4b-124">tooconfigure hello integration of ArcGIS Online into Azure AD, you need tooadd ArcGIS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="77e4b-125">**tooadd ArcGIS 線上 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77e4b-125">**tooadd ArcGIS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e4b-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="77e4b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="77e4b-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="77e4b-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="77e4b-131">按一下**新的應用程式**上 hello hello 對話方塊 tooadd 新應用程式頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="77e4b-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="77e4b-133">在 [hello] 搜尋方塊中，輸入**ArcGIS 線上**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-133">In hello search box, type **ArcGIS Online**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="77e4b-135">在 hello 結果 窗格中，選取  **ArcGIS 線上**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77e4b-135">In hello results panel, select **ArcGIS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="77e4b-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77e4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="77e4b-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ArcGIS Online 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77e4b-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="77e4b-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 ArcGIS 線上中是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="77e4b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ArcGIS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="77e4b-140">換句話說，Azure AD 使用者與 hello ArcGIS 線上中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="77e4b-140">In other words, a link relationship between an Azure AD user and hello related user in ArcGIS Online needs toobe established.</span></span>

<span data-ttu-id="77e4b-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** ArcGIS 線上中。</span><span class="sxs-lookup"><span data-stu-id="77e4b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="77e4b-142">tooconfigure 和測試 Azure AD 單一登入與 ArcGIS Online，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-142">tooconfigure and test Azure AD single sign-on with ArcGIS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="77e4b-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="77e4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="77e4b-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="77e4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="77e4b-145">**[建立線上 ArcGIS 的測試使用者](#creating-an-arcgis-online-test-user)** -toohave 許 Simon ArcGIS Online 連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="77e4b-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - toohave a counterpart of Britta Simon in ArcGIS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="77e4b-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77e4b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="77e4b-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="77e4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="77e4b-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="77e4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="77e4b-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入 ArcGIS 線上應用程式中。</span><span class="sxs-lookup"><span data-stu-id="77e4b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="77e4b-150">**tooconfigure Azure AD 單一登入與 ArcGIS Online，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77e4b-150">**tooconfigure Azure AD single sign-on with ArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e4b-151">在 Azure 入口網站上 hello hello **ArcGIS 線上**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-151">In hello Azure portal, on hello **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="77e4b-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77e4b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="77e4b-155">在 hello **ArcGIS 線上網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-155">On hello **ArcGIS Online Domain and URLs** section, perform hello following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="77e4b-157">在 hello**登入 URL**文字方塊中，使用下列模式的 hello 類型 hello 值：`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="77e4b-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="77e4b-158">這個值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="77e4b-158">This value is not hello real.</span></span> <span data-ttu-id="77e4b-159">更新此值以 hello 實際的登入 URL。</span><span class="sxs-lookup"><span data-stu-id="77e4b-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="77e4b-160">請連絡[ArcGIS 線上的用戶端支援小組](http://support.esri.com/)tooget 此值。</span><span class="sxs-lookup"><span data-stu-id="77e4b-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) tooget this value.</span></span> 

4. <span data-ttu-id="77e4b-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="77e4b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="77e4b-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="77e4b-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="77e4b-165">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ArcGIS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="77e4b-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="77e4b-166">按一下 [編輯設定]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="77e4b-167">![編輯設定](./media/active-directory-saas-arcgis-tutorial/ic784742.png "編輯設定")</span><span class="sxs-lookup"><span data-stu-id="77e4b-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="77e4b-168">按一下 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="77e4b-168">Click **Security**.</span></span>

    <span data-ttu-id="77e4b-169">![安全性](./media/active-directory-saas-arcgis-tutorial/ic784743.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="77e4b-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="77e4b-170">在 [企業登入] 下方，按一下 [設定識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="77e4b-171">![企業登入](./media/active-directory-saas-arcgis-tutorial/ic784744.png "企業登入")</span><span class="sxs-lookup"><span data-stu-id="77e4b-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="77e4b-172">在 hello**設定身分識別提供者**組態頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-172">On hello **Set Identity Provider** configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="77e4b-173">![設定識別提供者](./media/active-directory-saas-arcgis-tutorial/ic784745.png "設定識別提供者")</span><span class="sxs-lookup"><span data-stu-id="77e4b-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="77e4b-174">a.</span><span class="sxs-lookup"><span data-stu-id="77e4b-174">a.</span></span> <span data-ttu-id="77e4b-175">在 hello**名稱**文字方塊中，輸入您的組織名稱。</span><span class="sxs-lookup"><span data-stu-id="77e4b-175">In hello **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="77e4b-176">b.</span><span class="sxs-lookup"><span data-stu-id="77e4b-176">b.</span></span> <span data-ttu-id="77e4b-177">如**hello 企業身分識別提供者的中繼資料，才會提供使用**，選取**檔案**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-177">For **Metadata for hello Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="77e4b-178">c.</span><span class="sxs-lookup"><span data-stu-id="77e4b-178">c.</span></span> <span data-ttu-id="77e4b-179">tooupload 您下載的中繼資料檔案中，按一下 **選擇檔案**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-179">tooupload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="77e4b-180">d.</span><span class="sxs-lookup"><span data-stu-id="77e4b-180">d.</span></span> <span data-ttu-id="77e4b-181">按一下 [設定識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="77e4b-182">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="77e4b-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="77e4b-183">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="77e4b-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="77e4b-184">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="77e4b-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="77e4b-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77e4b-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="77e4b-186">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="77e4b-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="77e4b-188">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77e4b-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e4b-189">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="77e4b-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="77e4b-191">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="77e4b-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="77e4b-193">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="77e4b-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="77e4b-195">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="77e4b-197">a.</span><span class="sxs-lookup"><span data-stu-id="77e4b-197">a.</span></span> <span data-ttu-id="77e4b-198">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="77e4b-199">b.</span><span class="sxs-lookup"><span data-stu-id="77e4b-199">b.</span></span> <span data-ttu-id="77e4b-200">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="77e4b-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="77e4b-201">c.</span><span class="sxs-lookup"><span data-stu-id="77e4b-201">c.</span></span> <span data-ttu-id="77e4b-202">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="77e4b-203">d.</span><span class="sxs-lookup"><span data-stu-id="77e4b-203">d.</span></span> <span data-ttu-id="77e4b-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="77e4b-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="77e4b-205">建立 ArcGIS Online 測試使用者</span><span class="sxs-lookup"><span data-stu-id="77e4b-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="77e4b-206">在順序 tooenable Azure AD 使用者 toolog 入 ArcGIS Online，您必須是佈建到 ArcGIS 線上。</span><span class="sxs-lookup"><span data-stu-id="77e4b-206">In order tooenable Azure AD users toolog into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="77e4b-207">在 ArcGIS 線上 hello 情況下，佈建須手動進行。</span><span class="sxs-lookup"><span data-stu-id="77e4b-207">In hello case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="77e4b-208">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77e4b-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e4b-209">登入 tooyour **ArcGIS**租用戶。</span><span class="sxs-lookup"><span data-stu-id="77e4b-209">Log in tooyour **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="77e4b-210">按一下 [邀請成員]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="77e4b-211">![邀請成員](./media/active-directory-saas-arcgis-tutorial/ic784747.png "邀請成員")</span><span class="sxs-lookup"><span data-stu-id="77e4b-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="77e4b-212">選取 [自動新增成員而不傳送電子郵件]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="77e4b-213">![自動新增成員](./media/active-directory-saas-arcgis-tutorial/ic784748.png "自動新增成員")</span><span class="sxs-lookup"><span data-stu-id="77e4b-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="77e4b-214">在 hello**成員**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77e4b-214">On hello **Members** dialog page, perform hello following steps:</span></span>
   
     <span data-ttu-id="77e4b-215">![新增並檢閱](./media/active-directory-saas-arcgis-tutorial/ic784749.png "新增並檢閱")</span><span class="sxs-lookup"><span data-stu-id="77e4b-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="77e4b-216">a.</span><span class="sxs-lookup"><span data-stu-id="77e4b-216">a.</span></span> <span data-ttu-id="77e4b-217">輸入 hello**電子郵件**，**名字**，和**姓氏**想 tooprovision 之有效 AAD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="77e4b-217">Enter hello **Email**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision.</span></span>
  
     <span data-ttu-id="77e4b-218">b.</span><span class="sxs-lookup"><span data-stu-id="77e4b-218">b.</span></span> <span data-ttu-id="77e4b-219">按一下 [新增並檢閱]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="77e4b-220">檢閱您所輸入，然後按一下 hello 資料**新增成員**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-220">Review hello data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="77e4b-221">![新增成員](./media/active-directory-saas-arcgis-tutorial/ic784750.png "新增成員")</span><span class="sxs-lookup"><span data-stu-id="77e4b-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="77e4b-222">hello Azure Active Directory 帳戶持有者將收到一封電子郵件，並遵循連結 tooconfirm 他們的帳戶之前就會生效。</span><span class="sxs-lookup"><span data-stu-id="77e4b-222">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="77e4b-223">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="77e4b-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="77e4b-224">在本節中，您可以授與存取 tooArcGIS 線上啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="77e4b-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooArcGIS Online.</span></span>

![指派使用者][200] 

<span data-ttu-id="77e4b-226">**tooassign 許 Simon tooArcGIS 上線，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="77e4b-226">**tooassign Britta Simon tooArcGIS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="77e4b-227">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="77e4b-229">在 [hello] 應用程式清單中，選取**ArcGIS 線上**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-229">In hello applications list, select **ArcGIS Online**.</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="77e4b-231">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="77e4b-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="77e4b-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77e4b-233">Click **Add** button.</span></span> <span data-ttu-id="77e4b-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="77e4b-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="77e4b-236">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="77e4b-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="77e4b-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77e4b-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="77e4b-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="77e4b-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="77e4b-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="77e4b-239">Testing single sign-on</span></span>

<span data-ttu-id="77e4b-240">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="77e4b-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="77e4b-241">當您按一下 hello ArcGIS 線上磚 hello 存取面板中的時，您應該取得自動登入 tooyour ArcGIS 線上應用程式。</span><span class="sxs-lookup"><span data-stu-id="77e4b-241">When you click hello ArcGIS Online tile in hello Access Panel, you should get automatically signed-on tooyour ArcGIS Online application.</span></span>
<span data-ttu-id="77e4b-242">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="77e4b-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="77e4b-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="77e4b-243">Additional resources</span></span>

* [<span data-ttu-id="77e4b-244">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77e4b-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="77e4b-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="77e4b-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

