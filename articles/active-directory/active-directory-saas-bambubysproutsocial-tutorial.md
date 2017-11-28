---
title: "教學課程：Azure Active Directory 與 Bambu by Sprout Social 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與透過社交發芽 Bambu 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="dc7ae-103">教學課程：Azure Active Directory 與 Bambu by Sprout Social 整合</span><span class="sxs-lookup"><span data-stu-id="dc7ae-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="dc7ae-104">在此教學課程中，您學會如何 toointegrate Bambu 由發芽社交與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc7ae-105">與 Azure AD 整合的社交發芽 Bambu 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dc7ae-106">您可以控制存取 tooBambu 發芽社交由 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="dc7ae-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="dc7ae-107">您可以使用其 Azure AD 帳戶啟用您使用者 tooautomatically get 登入 tooBambu 由發芽社交 （單一登入）</span><span class="sxs-lookup"><span data-stu-id="dc7ae-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc7ae-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="dc7ae-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="dc7ae-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="dc7ae-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="dc7ae-110">Prerequisites</span></span>

<span data-ttu-id="dc7ae-111">tooconfigure Azure AD 與 Bambu 由發芽社交整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="dc7ae-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dc7ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc7ae-113">啟用 Bambu by Sprout Social 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="dc7ae-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc7ae-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc7ae-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="dc7ae-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc7ae-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="dc7ae-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc7ae-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="dc7ae-118">Scenario description</span></span>
<span data-ttu-id="dc7ae-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc7ae-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="dc7ae-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc7ae-121">加入透過社交發芽 Bambu 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="dc7ae-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="dc7ae-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dc7ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="dc7ae-123">加入透過社交發芽 Bambu 從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="dc7ae-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="dc7ae-124">tooconfigure hello 整合的社交發芽 Bambu 到 Azure AD，您需要 tooadd 由發芽社交 Bambu hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dc7ae-125">**tooadd Bambu 由發芽社交 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dc7ae-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc7ae-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc7ae-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dc7ae-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="dc7ae-131">按一下**新的應用程式**上 hello hello 對話方塊 tooadd 新應用程式頂端的按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="dc7ae-133">在 [hello] 搜尋方塊中，輸入**由發芽社交 Bambu**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="dc7ae-135">在 hello [結果] 窗格中，選取**由發芽社交 Bambu**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc7ae-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dc7ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc7ae-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Bambu by Sprout Social 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc7ae-139">單一登入 toowork，Azure AD 需要 tooknow 哪些 hello 對應項目中的使用者透過社交發芽 Bambu 都 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="dc7ae-140">換句話說，Azure AD 使用者與中的社交發芽 Bambu hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="dc7ae-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**使用者名稱**中透過社交發芽 Bambu。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="dc7ae-142">tooconfigure 及透過社交發芽 Bambu 與 Azure AD 單一登入測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dc7ae-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dc7ae-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc7ae-145">**[建立由發芽社交測試使用者 Bambu](#creating-a-bambu-by-sprout-social-test-user)**  -toohave 許 Simon 中 Bambu 由發芽社交連結的 toohello Azure AD 表示她的對應項目。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="dc7ae-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc7ae-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc7ae-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="dc7ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc7ae-149">在本節中，您啟用 Azure AD 單一登入 hello Azure 入口網站中，並設定單一登入在您 Bambu 發芽社交應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="dc7ae-150">**社交發芽 Bambu 與 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dc7ae-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc7ae-151">在 Azure 入口網站上 hello hello **Bambu 由發芽社交**應用程式整合頁面上，按一下**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="dc7ae-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="dc7ae-155">在 hello**發芽社交網域和 Url Bambu**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="dc7ae-157">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="dc7ae-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="dc7ae-161">在 hello**發芽社交組態 Bambu**區段中，按一下**設定 Bambu 由發芽社交**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="dc7ae-162">複製 hello **SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="dc7ae-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="dc7ae-164">tooconfigure 單一登入上**由發芽社交 Bambu**端，您需要下載 toosend hello**中繼資料 XML**和**SAML 單一登入服務 URL**太[發芽社交支援 Bambu](mailto:support@getbambu.com)。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="dc7ae-165">它們會設定此順序 toohave hello SAML SSO 連線兩端上正確設定。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="dc7ae-166">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="dc7ae-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="dc7ae-167">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="dc7ae-168">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="dc7ae-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc7ae-169">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dc7ae-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc7ae-170">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="dc7ae-172">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="dc7ae-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc7ae-173">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc7ae-175">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc7ae-177">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc7ae-179">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc7ae-181">a.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-181">a.</span></span> <span data-ttu-id="dc7ae-182">在 hello**名稱**文字方塊中，輸入**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="dc7ae-183">b.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-183">b.</span></span> <span data-ttu-id="dc7ae-184">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**許 Simon。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="dc7ae-185">c.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-185">c.</span></span> <span data-ttu-id="dc7ae-186">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dc7ae-187">d.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-187">d.</span></span> <span data-ttu-id="dc7ae-188">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="dc7ae-189">建立 Bambu by Sprout Social 測試使用者</span><span class="sxs-lookup"><span data-stu-id="dc7ae-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="dc7ae-190">應用程式支援恰好在即時使用者佈建，以及之後驗證的使用者將會在 hello 應用程式中自動建立。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dc7ae-191">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="dc7ae-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dc7ae-192">在本節中，您可以授與的社交發芽她存取 tooBambu 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![指派使用者][200] 

<span data-ttu-id="dc7ae-194">**tooassign 由發芽社交許 Simon tooBambu 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="dc7ae-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="dc7ae-195">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="dc7ae-197">在 [hello] 應用程式清單中，選取**由發芽社交 Bambu**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="dc7ae-199">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="dc7ae-201">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-201">Click **Add** button.</span></span> <span data-ttu-id="dc7ae-202">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="dc7ae-204">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dc7ae-205">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc7ae-206">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc7ae-207">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="dc7ae-207">Testing single sign-on</span></span>

<span data-ttu-id="dc7ae-208">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dc7ae-209">當您按一下 hello Bambu 由發芽社交圖格 hello 存取面板中時，您應該取得自動登入 tooyour Bambu 發芽社交應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="dc7ae-210">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="dc7ae-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dc7ae-211">其他資源</span><span class="sxs-lookup"><span data-stu-id="dc7ae-211">Additional resources</span></span>

* [<span data-ttu-id="dc7ae-212">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc7ae-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc7ae-213">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="dc7ae-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

