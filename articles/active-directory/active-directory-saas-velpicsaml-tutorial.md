---
title: "教學課程：Azure Active Directory 與 Velpic SAML 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Velpic SAML 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 613947d8fe95113382a2cdc0f79ce9eda85a0127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="79291-103">教學課程：Azure Active Directory 與 Velpic SAML 整合</span><span class="sxs-lookup"><span data-stu-id="79291-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="79291-104">在此教學課程中，您學會如何 toointegrate Velpic SAML 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="79291-104">In this tutorial, you learn how toointegrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79291-105">與 Azure AD 整合 Velpic SAML 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="79291-105">Integrating Velpic SAML with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79291-106">您可以控制存取 tooVelpic SAML 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="79291-106">You can control in Azure AD who has access tooVelpic SAML</span></span>
- <span data-ttu-id="79291-107">您可以啟用您的使用者 tooautomatically get 登入 tooVelpic SAML （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="79291-107">You can enable your users tooautomatically get signed-on tooVelpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79291-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="79291-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="79291-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="79291-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79291-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="79291-110">Prerequisites</span></span>

<span data-ttu-id="79291-111">tooconfigure Azure AD 與 Velpic SAML 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="79291-111">tooconfigure Azure AD integration with Velpic SAML, you need hello following items:</span></span>

- <span data-ttu-id="79291-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="79291-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79291-113">啟用 Velpic SAML 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="79291-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79291-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="79291-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79291-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="79291-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79291-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="79291-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="79291-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="79291-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79291-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="79291-118">Scenario description</span></span>
<span data-ttu-id="79291-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79291-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79291-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="79291-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79291-121">從 hello 圖庫加入 Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="79291-121">Adding Velpic SAML from hello gallery</span></span>
2. <span data-ttu-id="79291-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="79291-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-hello-gallery"></a><span data-ttu-id="79291-123">從 hello 圖庫加入 Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="79291-123">Adding Velpic SAML from hello gallery</span></span>
<span data-ttu-id="79291-124">tooconfigure hello 整合 Velpic SAML 到 Azure AD，您需要 tooadd Velpic SAML hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="79291-124">tooconfigure hello integration of Velpic SAML into Azure AD, you need tooadd Velpic SAML from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79291-125">**tooadd Velpic SAML 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79291-125">**tooadd Velpic SAML from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79291-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="79291-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79291-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="79291-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79291-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="79291-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="79291-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="79291-133">在 [hello] 搜尋方塊中，輸入**Velpic SAML**。</span><span class="sxs-lookup"><span data-stu-id="79291-133">In hello search box, type **Velpic SAML**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="79291-135">在 hello 結果 窗格中，選取  **Velpic SAML**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="79291-135">In hello results panel, select **Velpic SAML**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79291-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="79291-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79291-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Velpic SAML 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79291-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="79291-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者 Velpic saml 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="79291-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Velpic SAML is tooa user in Azure AD.</span></span> <span data-ttu-id="79291-140">換句話說，Azure AD 使用者與 hello Velpic saml 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="79291-140">In other words, a link relationship between an Azure AD user and hello related user in Velpic SAML needs toobe established.</span></span>

<span data-ttu-id="79291-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Velpic saml。</span><span class="sxs-lookup"><span data-stu-id="79291-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Velpic SAML.</span></span>

<span data-ttu-id="79291-142">tooconfigure 及 Velpic SAML 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="79291-142">tooconfigure and test Azure AD single sign-on with Velpic SAML, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79291-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="79291-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79291-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="79291-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79291-145">**[建立測試使用者 Velpic SAML](#creating-a-velpic-saml-test-user)**  -toohave 許 Simon Velpic saml 連結的 toohello Azure AD 表示她的對應項目。</span><span class="sxs-lookup"><span data-stu-id="79291-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - toohave a counterpart of Britta Simon in Velpic SAML that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="79291-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79291-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79291-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="79291-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79291-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="79291-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79291-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並 Velpic SAML 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="79291-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="79291-150">**tooconfigure Azure AD 單一登入與 Velpic SAML，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79291-150">**tooconfigure Azure AD single sign-on with Velpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="79291-151">在 hello Azure 管理入口網站上 hello **Velpic SAML**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="79291-151">In hello Azure Management portal, on hello **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="79291-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79291-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="79291-155">輸入 hello 詳細資料中 hello **Velpic SAML 網域和 Url**區段-</span><span class="sxs-lookup"><span data-stu-id="79291-155">Enter hello details in hello **Velpic SAML Domain and URLs** section-</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="79291-157">a.</span><span class="sxs-lookup"><span data-stu-id="79291-157">a.</span></span> <span data-ttu-id="79291-158">在 hello**登入 URL**文字方塊中，做為型別 hello 值：`https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="79291-158">In hello **Sign-on URL** textbox, type hello value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="79291-159">b.</span><span class="sxs-lookup"><span data-stu-id="79291-159">b.</span></span> <span data-ttu-id="79291-160">在 hello**識別碼**文字方塊中，貼上 hello **'的單一登入 URL'**值`https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="79291-160">In hello **Identifier** textbox, paste hello **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="79291-161">請注意，將由 hello Velpic SAML 小組提供 hello 登入 URL 識別項的值可設定 hello SSO 外掛程式 Velpic SAML 端時。</span><span class="sxs-lookup"><span data-stu-id="79291-161">Please note that hello Sign on URL will be provided by hello Velpic SAML team and Identifier value will be available when you configure hello SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="79291-162">您需要 toocopy 來自 Velpic SAML 應用程式頁面上的值並貼至此處。</span><span class="sxs-lookup"><span data-stu-id="79291-162">You need toocopy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="79291-163">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello XML 檔案。</span><span class="sxs-lookup"><span data-stu-id="79291-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="79291-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-165">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="79291-167">在 hello Velpic SAML 組態] 區段中，按一下 [設定 Velpic SAML tooopen 設定登入視窗。</span><span class="sxs-lookup"><span data-stu-id="79291-167">On hello Velpic SAML Configuration section, click Configure Velpic SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="79291-168">複製 hello 快速參考 > 一節中的 hello SAML 實體識別碼。</span><span class="sxs-lookup"><span data-stu-id="79291-168">Copy hello SAML Entity ID from hello Quick Reference section.</span></span>

7. <span data-ttu-id="79291-169">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Velpic SAML 公司網站。</span><span class="sxs-lookup"><span data-stu-id="79291-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="79291-170">按一下**管理**索引標籤上，並移過**整合**區段需要 tooclick**外掛程式**登入按鈕 toocreate 新外掛程式。</span><span class="sxs-lookup"><span data-stu-id="79291-170">Click on **Manage** tab and go too**Integration** section where you need tooclick on **Plugins** button toocreate new plugin for Sign-In.</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="79291-172">按一下 hello **'加入外掛程式'**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-172">Click on hello **‘Add plugin’** button.</span></span>
    
    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="79291-174">按一下 hello **SAML**磚 hello 新增外掛程式網頁中。</span><span class="sxs-lookup"><span data-stu-id="79291-174">Click on hello **SAML** tile in hello Add Plugin page.</span></span>
    
    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="79291-176">輸入新 SAML 外掛程式 hello hello 名稱，然後按一下 hello **'Add'**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-176">Enter hello name of hello new SAML plugin and click hello **‘Add’** button.</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="79291-178">輸入 hello 詳細資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="79291-178">Enter hello details as follows:</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="79291-180">a.</span><span class="sxs-lookup"><span data-stu-id="79291-180">a.</span></span> <span data-ttu-id="79291-181">在 hello**名稱**文字方塊中，型別 hello SAML 外掛程式名稱。</span><span class="sxs-lookup"><span data-stu-id="79291-181">In hello **Name** textbox, type hello name of SAML plugin.</span></span>

    <span data-ttu-id="79291-182">b.</span><span class="sxs-lookup"><span data-stu-id="79291-182">b.</span></span> <span data-ttu-id="79291-183">在 hello**簽發者 URL**文字方塊中，貼上 hello **SAML 實體識別碼**您所複製的 hello**設定登入**hello Azure 入口網站視窗。</span><span class="sxs-lookup"><span data-stu-id="79291-183">In hello **Issuer URL** textbox, paste hello **SAML Entity ID** you copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="79291-184">c.</span><span class="sxs-lookup"><span data-stu-id="79291-184">c.</span></span> <span data-ttu-id="79291-185">在 hello**提供者中繼資料組態**上載 hello 中繼資料 XML 檔案，您從 Azure 入口網站下載檔案。</span><span class="sxs-lookup"><span data-stu-id="79291-185">In hello **Provider Metadata Config** upload hello Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="79291-186">d.</span><span class="sxs-lookup"><span data-stu-id="79291-186">d.</span></span> <span data-ttu-id="79291-187">您也可以選擇 tooenable SAML 即時佈建藉由啟用 hello **'自動建立新的使用者'**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="79291-187">You can also choose tooenable SAML just in time provisioning by enabling hello **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="79291-188">如果使用者不存在於 Velpic，而且沒有啟用這個旗標，從 Azure 的 hello 登入將會失敗。</span><span class="sxs-lookup"><span data-stu-id="79291-188">If a user doesn’t exist in Velpic and this flag is not enabled, hello login from Azure will fail.</span></span> <span data-ttu-id="79291-189">如果 hello 旗標已啟用的 hello 使用者會自動佈建到 Velpic 在 hello 登入時間。</span><span class="sxs-lookup"><span data-stu-id="79291-189">If hello flag is enabled hello user will automatically be provisioned into Velpic at hello time of login.</span></span> 

    <span data-ttu-id="79291-190">e.</span><span class="sxs-lookup"><span data-stu-id="79291-190">e.</span></span> <span data-ttu-id="79291-191">複製 hello**單一登入 URL**從 hello 文字方塊中，然後貼上在 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="79291-191">Copy hello **Single sign on URL** from hello text box and paste it in hello Azure portal.</span></span>
    
    <span data-ttu-id="79291-192">f.</span><span class="sxs-lookup"><span data-stu-id="79291-192">f.</span></span> <span data-ttu-id="79291-193">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="79291-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79291-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="79291-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="79291-195">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="79291-195">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="79291-197">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79291-197">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79291-198">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="79291-198">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79291-200">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="79291-200">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79291-202">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="79291-202">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79291-204">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="79291-204">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79291-206">a.</span><span class="sxs-lookup"><span data-stu-id="79291-206">a.</span></span> <span data-ttu-id="79291-207">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="79291-207">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79291-208">b.</span><span class="sxs-lookup"><span data-stu-id="79291-208">b.</span></span> <span data-ttu-id="79291-209">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="79291-209">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79291-210">c.</span><span class="sxs-lookup"><span data-stu-id="79291-210">c.</span></span> <span data-ttu-id="79291-211">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="79291-211">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79291-212">d.</span><span class="sxs-lookup"><span data-stu-id="79291-212">d.</span></span> <span data-ttu-id="79291-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="79291-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="79291-214">建立 Velpic SAML 測試使用者</span><span class="sxs-lookup"><span data-stu-id="79291-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="79291-215">此步驟為通常不需要 hello 應用程式支援即時使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="79291-215">This step is usually not required as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="79291-216">如果未啟用 hello 自動使用者佈建然後建立手動使用者即可，如下所述。</span><span class="sxs-lookup"><span data-stu-id="79291-216">If hello automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="79291-217">以系統管理員身分登入您的 Velpic SAML 公司網站，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="79291-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="79291-218">按一下 管理 索引標籤上並移 tooUsers 區段中，然後按一下新按鈕 tooadd 使用者。</span><span class="sxs-lookup"><span data-stu-id="79291-218">Click on Manage tab and go tooUsers section, then click on New button tooadd users.</span></span>

    ![新增使用者](./media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="79291-220">在 hello **「 建立新的使用者 」**對話方塊頁面上，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="79291-220">On hello **“Create New User”** dialog page, perform hello following steps.</span></span>

    ![user](./media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="79291-222">a.</span><span class="sxs-lookup"><span data-stu-id="79291-222">a.</span></span> <span data-ttu-id="79291-223">在 hello**名字**文字方塊中，類型許 Simon 的 hello 名字。</span><span class="sxs-lookup"><span data-stu-id="79291-223">In hello **First Name** textbox, type hello first name of Britta Simon.</span></span>

    <span data-ttu-id="79291-224">b.</span><span class="sxs-lookup"><span data-stu-id="79291-224">b.</span></span> <span data-ttu-id="79291-225">在 hello**姓氏**文字方塊中，類型許 Simon 的 hello 最後一個名稱。</span><span class="sxs-lookup"><span data-stu-id="79291-225">In hello **Last Name** textbox, type hello last name of Britta Simon.</span></span>

    <span data-ttu-id="79291-226">c.</span><span class="sxs-lookup"><span data-stu-id="79291-226">c.</span></span> <span data-ttu-id="79291-227">在 hello**使用者名**文字方塊中，輸入 hello 的使用者名稱，Simon 許。</span><span class="sxs-lookup"><span data-stu-id="79291-227">In hello **User Name** textbox, type hello user name of Britta Simon.</span></span>

    <span data-ttu-id="79291-228">d.</span><span class="sxs-lookup"><span data-stu-id="79291-228">d.</span></span> <span data-ttu-id="79291-229">在 [hello**電子郵件**許 Simon 帳戶類型 hello 電子郵件地址] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="79291-229">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="79291-230">e.</span><span class="sxs-lookup"><span data-stu-id="79291-230">e.</span></span> <span data-ttu-id="79291-231">其餘的 hello 資訊是選擇性的您可以填入必要的。</span><span class="sxs-lookup"><span data-stu-id="79291-231">Rest of hello information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="79291-232">f.</span><span class="sxs-lookup"><span data-stu-id="79291-232">f.</span></span> <span data-ttu-id="79291-233">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="79291-233">Click **SAVE**.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79291-234">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="79291-234">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79291-235">在本節中，您可以授與他們存取 tooVelpic SAML 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="79291-235">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooVelpic SAML.</span></span>

![指派使用者][200] 

<span data-ttu-id="79291-237">**tooassign 許 Simon tooVelpic SAML，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="79291-237">**tooassign Britta Simon tooVelpic SAML, perform hello following steps:**</span></span>

1. <span data-ttu-id="79291-238">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="79291-238">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="79291-240">在 [hello] 應用程式清單中，選取**Velpic SAML**。</span><span class="sxs-lookup"><span data-stu-id="79291-240">In hello applications list, select **Velpic SAML**.</span></span>

    ![設定單一登入](./media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="79291-242">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="79291-242">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="79291-244">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-244">Click **Add** button.</span></span> <span data-ttu-id="79291-245">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="79291-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="79291-247">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="79291-247">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79291-248">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79291-249">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79291-250">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="79291-250">Testing single sign-on</span></span>

<span data-ttu-id="79291-251">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="79291-251">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="79291-252">當您按一下的 hello Velpic SAML 磚 hello 存取面板中時，您應該取得 Velpic SAML 應用程式的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="79291-252">When you click hello Velpic SAML tile in hello Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="79291-253">您應該會看見 hello **'登入 Azure AD'** hello 登入頁面上的按鈕。</span><span class="sxs-lookup"><span data-stu-id="79291-253">You should see hello **‘Log In With Azure AD’** button on hello sign in page.</span></span>

    ![外掛程式](./media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="79291-255">按一下 hello **'登入 Azure AD'**按鈕 toolog tooVelpic 使用 Azure AD 帳戶中的。</span><span class="sxs-lookup"><span data-stu-id="79291-255">Click on hello **‘Log In With Azure AD’** button toolog in tooVelpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="79291-256">其他資源</span><span class="sxs-lookup"><span data-stu-id="79291-256">Additional resources</span></span>

* [<span data-ttu-id="79291-257">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79291-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79291-258">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="79291-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png

