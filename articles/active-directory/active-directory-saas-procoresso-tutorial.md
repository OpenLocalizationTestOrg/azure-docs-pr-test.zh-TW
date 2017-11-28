---
title: "教學課程：Azure Active Directory 與 Procore SSO 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Procore SSO 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a><span data-ttu-id="d2cdd-103">教學課程：Azure Active Directory 與 Procore SSO 整合</span><span class="sxs-lookup"><span data-stu-id="d2cdd-103">Tutorial: Azure Active Directory integration with Procore SSO</span></span>

<span data-ttu-id="d2cdd-104">在此教學課程中，您學會如何 toointegrate Procore SSO 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-104">In this tutorial, you learn how toointegrate Procore SSO with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2cdd-105">與 Azure AD 整合 Procore SSO 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="d2cdd-105">Integrating Procore SSO with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d2cdd-106">您可以控制存取 tooProcore SSO 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="d2cdd-106">You can control in Azure AD who has access tooProcore SSO</span></span>
- <span data-ttu-id="d2cdd-107">您可以啟用您的使用者 tooautomatically get 登入 tooProcore SSO （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="d2cdd-107">You can enable your users tooautomatically get signed-on tooProcore SSO (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2cdd-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="d2cdd-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d2cdd-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="d2cdd-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d2cdd-110">Prerequisites</span></span>

<span data-ttu-id="d2cdd-111">tooconfigure Procore SSO 與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="d2cdd-111">tooconfigure Azure AD integration with Procore SSO, you need hello following items:</span></span>

- <span data-ttu-id="d2cdd-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d2cdd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2cdd-113">已啟用 Procore SSO 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d2cdd-113">A Procore SSO single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d2cdd-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d2cdd-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d2cdd-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2cdd-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d2cdd-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d2cdd-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d2cdd-118">Scenario description</span></span>
<span data-ttu-id="d2cdd-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d2cdd-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d2cdd-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2cdd-121">從 hello 圖庫加入 Procore SSO</span><span class="sxs-lookup"><span data-stu-id="d2cdd-121">Adding Procore SSO from hello gallery</span></span>
2. <span data-ttu-id="d2cdd-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d2cdd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-procore-sso-from-hello-gallery"></a><span data-ttu-id="d2cdd-123">從 hello 圖庫加入 Procore SSO</span><span class="sxs-lookup"><span data-stu-id="d2cdd-123">Adding Procore SSO from hello gallery</span></span>
<span data-ttu-id="d2cdd-124">tooconfigure hello 整合 Procore SSO 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Procore SSO。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-124">tooconfigure hello integration of Procore SSO into Azure AD, you need tooadd Procore SSO from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d2cdd-125">**tooadd Procore SSO hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d2cdd-125">**tooadd Procore SSO from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2cdd-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d2cdd-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d2cdd-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d2cdd-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d2cdd-133">在 [hello] 搜尋方塊中，輸入**Procore SSO**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-133">In hello search box, type **Procore SSO**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. <span data-ttu-id="d2cdd-135">在 hello 結果 窗格中，選取  **Procore SSO**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-135">In hello results panel, select **Procore SSO**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d2cdd-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d2cdd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d2cdd-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Procore SSO 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-138">In this section, you configure and test Azure AD single sign-on with Procore SSO based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d2cdd-139">單一登入 toowork，Azure AD 需要 tooknow Procore SSO 中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Procore SSO is tooa user in Azure AD.</span></span> <span data-ttu-id="d2cdd-140">換句話說，Azure AD 使用者與 hello Procore SSO 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-140">In other words, a link relationship between an Azure AD user and hello related user in Procore SSO needs toobe established.</span></span>

<span data-ttu-id="d2cdd-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Procore SSO 中。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Procore SSO.</span></span>

<span data-ttu-id="d2cdd-142">tooconfigure 及測試 Azure AD 單一登入與 Procore SSO，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="d2cdd-142">tooconfigure and test Azure AD single sign-on with Procore SSO, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d2cdd-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d2cdd-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2cdd-145">**[建立測試使用者 Procore SSO](#creating-a-procore-sso-test-user)**  -toohave 許 Simon Procore SSO 是連結的 toohello Azure AD 的她的表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-145">**[Creating a Procore SSO test user](#creating-a-procore-sso-test-user)** - toohave a counterpart of Britta Simon in Procore SSO that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d2cdd-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2cdd-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d2cdd-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d2cdd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d2cdd-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Procore SSO 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Procore SSO application.</span></span>

<span data-ttu-id="d2cdd-150">**tooconfigure Azure AD 單一登入使用 Procore SSO，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d2cdd-150">**tooconfigure Azure AD single sign-on with Procore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2cdd-151">在 hello Azure 管理入口網站上 hello **Procore SSO**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-151">In hello Azure Management portal, on hello **Procore SSO** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d2cdd-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. <span data-ttu-id="d2cdd-155">在 hello **Procore SSO 網域和 Url**區段中，hello 使用者沒有 tooperform 任何步驟，因為與 Azure 已預先整合 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-155">On hello **Procore SSO Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. <span data-ttu-id="d2cdd-157">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. <span data-ttu-id="d2cdd-159">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-159">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d2cdd-161">在 hello **Procore SSO 組態**區段中，按一下**設定 Procore SSO** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-161">On hello **Procore SSO Configuration** section, click **Configure Procore SSO** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d2cdd-162">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="d2cdd-162">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. <span data-ttu-id="d2cdd-164">tooconfigure 單一登入上**Procore SSO**端時，系統管理員身分登入 tooyour procore 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-164">tooconfigure single sign-on on **Procore SSO** side, login tooyour procore company site as an administrator.</span></span>

8. <span data-ttu-id="d2cdd-165">從 hello 工具箱卸除向下，按一下 [ **Admin** tooopen hello SSO 設定] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-165">From hello toolbox drop down, click on **Admin** tooopen hello SSO settings page.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. <span data-ttu-id="d2cdd-167">貼上的 hello 值為 hello 方塊中所述以下-</span><span class="sxs-lookup"><span data-stu-id="d2cdd-167">Paste hello values in hello boxes as described below-</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    <span data-ttu-id="d2cdd-169">a.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-169">a.</span></span> <span data-ttu-id="d2cdd-170">在 hello**單一登入簽發者 URL**方塊中，貼上從 hello Azure 入口網站複製 SAML 實體識別碼 hello。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-170">In hello **Single Sign On Issuer URL** box, paste hello SAML Entity ID copied from hello Azure portal.</span></span>

    <span data-ttu-id="d2cdd-171">b.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-171">b.</span></span> <span data-ttu-id="d2cdd-172">在 hello **SAML 登入目標 URL**方塊中，貼上的 hello 從 hello Azure 入口網站複製的 SAML 單一登入服務 URL。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-172">In hello **SAML Sign On Target URL** box, paste hello SAML Single Sign-On Service URL copied from hello Azure portal.</span></span>

    <span data-ttu-id="d2cdd-173">c.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-173">c.</span></span> <span data-ttu-id="d2cdd-174">現在開啟 hello**中繼資料 XML**上方 hello Azure 入口網站和名為 hello 標記中的複製 hello 憑證從下載**X509Certificate**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-174">Now open hello **Metadata XML** downloaded above from hello Azure portal and copy hello certficate in hello tag named **X509Certificate**.</span></span> <span data-ttu-id="d2cdd-175">貼上 hello 複製值到 hello**單一登入 x509 憑證**方塊。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-175">Paste hello copied value into hello **Single Sign On x509 Certificate** box.</span></span>

10. <span data-ttu-id="d2cdd-176">按一下 [儲存變更]。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-176">Click on **Save Changes**.</span></span>

11. <span data-ttu-id="d2cdd-177">這些設定之後，您需要 toosend hello**網域名稱**(例如**contoso.com**) 透過它您登入 Procore toohello [Procore 支援小組](https://support.procore.com/)，它們將啟動該網域同盟的 SSO。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-177">After these settings, you needs toosend hello **domain name** (e.g **contoso.com**) through which you are logging into Procore toohello [Procore Support team](https://support.procore.com/) and they will activate federated SSO for that domain.</span></span>

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d2cdd-178">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d2cdd-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="d2cdd-179">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-179">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d2cdd-181">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d2cdd-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2cdd-182">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-182">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d2cdd-184">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-184">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d2cdd-186">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-186">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2cdd-188">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="d2cdd-188">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d2cdd-190">a.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-190">a.</span></span> <span data-ttu-id="d2cdd-191">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-191">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d2cdd-192">b.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-192">b.</span></span> <span data-ttu-id="d2cdd-193">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-193">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d2cdd-194">c.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-194">c.</span></span> <span data-ttu-id="d2cdd-195">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-195">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d2cdd-196">d.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-196">d.</span></span> <span data-ttu-id="d2cdd-197">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-197">Click **Create**.</span></span>
 
### <a name="creating-a-procore-sso-test-user"></a><span data-ttu-id="d2cdd-198">建立 Procore SSO 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d2cdd-198">Creating a Procore SSO test user</span></span>

<span data-ttu-id="d2cdd-199">請遵循以下步驟 toocreate Procore 測試使用者的 hello 邊。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-199">Please follow hello below steps toocreate a Procore test user on their side.</span></span>

1. <span data-ttu-id="d2cdd-200">以系統管理員身分登入 tooyour procore 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-200">Login tooyour procore company site as an administrator.</span></span>  

2. <span data-ttu-id="d2cdd-201">從 hello 工具箱卸除向下，按一下 [**目錄**tooopen hello 公司目錄] 頁面。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-201">From hello toolbox drop down, click on **Directory** tooopen hello company directory page.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. <span data-ttu-id="d2cdd-203">按一下**新增人員**選項 tooopen hello 表單，並輸入下列選項-執行</span><span class="sxs-lookup"><span data-stu-id="d2cdd-203">Click on **Add a Person** option tooopen hello form and enter perform following options -</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    <span data-ttu-id="d2cdd-205">a.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-205">a.</span></span> <span data-ttu-id="d2cdd-206">在 hello**名字**文字方塊中，類型使用者的名字，例如**許**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-206">In hello **First Name** textbox, type user's first name like **Britta**.</span></span>

    <span data-ttu-id="d2cdd-207">b.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-207">b.</span></span> <span data-ttu-id="d2cdd-208">在 hello**姓氏**文字方塊中，類型使用者的姓氏，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-208">In hello **Last name** textbox, type user's last name like **Simon**.</span></span>

    <span data-ttu-id="d2cdd-209">c.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-209">c.</span></span> <span data-ttu-id="d2cdd-210">在 hello**電子郵件地址**文字方塊中，類型使用者的電子郵件地址喜歡 **BrittaSimon@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-210">In hello **Email Address** textbox, type user's email address like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="d2cdd-211">d.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-211">d.</span></span> <span data-ttu-id="d2cdd-212">將 [權限範本] 選取為 [稍後套用權限範本]。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-212">Select **Permission Template** as **Apply Permission Template Later**.</span></span>

    <span data-ttu-id="d2cdd-213">e.</span><span class="sxs-lookup"><span data-stu-id="d2cdd-213">e.</span></span> <span data-ttu-id="d2cdd-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-214">Click **Create**.</span></span>

4. <span data-ttu-id="d2cdd-215">檢查並更新如 hello 新增連絡人的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-215">Check and update hello details for hello newly added contact.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. <span data-ttu-id="d2cdd-217">按一下**儲存和傳送 Invitiation** （需要透過郵件邀請時） 或**儲存**（直接儲存） toocomplete hello 使用者註冊。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-217">Click on **Save and Send Invitiation** (if an invite through mail is required) or **Save** (Save directly) toocomplete hello user registration.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d2cdd-219">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="d2cdd-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d2cdd-220">在本節中，您可以授與他們存取 tooProcore SSO 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooProcore SSO.</span></span>

![指派使用者][200] 

<span data-ttu-id="d2cdd-222">**tooassign 許 Simon tooProcore SSO，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="d2cdd-222">**tooassign Britta Simon tooProcore SSO, perform hello following steps:**</span></span>

1. <span data-ttu-id="d2cdd-223">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d2cdd-225">在 [hello] 應用程式清單中，選取**Procore SSO**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-225">In hello applications list, select **Procore SSO**.</span></span>

    ![設定單一登入](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. <span data-ttu-id="d2cdd-227">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d2cdd-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-229">Click **Add** button.</span></span> <span data-ttu-id="d2cdd-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d2cdd-232">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d2cdd-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d2cdd-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d2cdd-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d2cdd-235">Testing single sign-on</span></span>

<span data-ttu-id="d2cdd-236">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d2cdd-237">如果要測試您的單一登入設定，請開啟存取面板。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-237">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="d2cdd-238">如需 [存取面板] 的詳細資訊，請參閱 [存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-238">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> <span data-ttu-id="d2cdd-239">當您按一下 hello Procore SSO 磚 hello 存取面板中的時，您應該取得自動登入 tooyour Procore SSO 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2cdd-239">When you click hello Procore SSO tile in hello Access Panel, you should get automatically signed-on tooyour Procore SSO application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d2cdd-240">其他資源</span><span class="sxs-lookup"><span data-stu-id="d2cdd-240">Additional resources</span></span>

* [<span data-ttu-id="d2cdd-241">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2cdd-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2cdd-242">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d2cdd-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

