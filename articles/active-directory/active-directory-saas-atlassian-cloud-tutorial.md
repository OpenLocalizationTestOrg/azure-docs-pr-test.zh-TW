---
title: "教學課程：Azure Active Directory 與 Atlassian Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Atlassian 雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: f679e8b3306bf0efb9373d8baa0cfe095b760aaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="a61b8-103">教學課程：Azure Active Directory 與 Atlassian Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="a61b8-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="a61b8-104">在此教學課程中，您學會如何 toointegrate Atlassian 雲端與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="a61b8-104">In this tutorial, you learn how toointegrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a61b8-105">與 Azure AD 整合 Atlassian 雲端可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="a61b8-105">Integrating Atlassian Cloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a61b8-106">您可以控制存取 tooAtlassian 雲端的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="a61b8-106">You can control in Azure AD who has access tooAtlassian Cloud</span></span>
- <span data-ttu-id="a61b8-107">您可以啟用您的使用者 tooautomatically get 登入 tooAtlassian （單一登入） 的雲端與他們的 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="a61b8-107">You can enable your users tooautomatically get signed-on tooAtlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a61b8-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a61b8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a61b8-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="a61b8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a61b8-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a61b8-110">Prerequisites</span></span>

<span data-ttu-id="a61b8-111">tooconfigure 與 Atlassian 雲端的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="a61b8-111">tooconfigure Azure AD integration with Atlassian Cloud, you need hello following items:</span></span>

- <span data-ttu-id="a61b8-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a61b8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a61b8-113">已啟用 Atlassian Cloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="a61b8-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a61b8-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="a61b8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a61b8-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="a61b8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a61b8-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="a61b8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a61b8-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="a61b8-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a61b8-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="a61b8-118">Scenario description</span></span>
<span data-ttu-id="a61b8-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a61b8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a61b8-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="a61b8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a61b8-121">從 hello 圖庫加入 Atlassian 雲端</span><span class="sxs-lookup"><span data-stu-id="a61b8-121">Adding Atlassian Cloud from hello gallery</span></span>
2. <span data-ttu-id="a61b8-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a61b8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-hello-gallery"></a><span data-ttu-id="a61b8-123">從 hello 圖庫加入 Atlassian 雲端</span><span class="sxs-lookup"><span data-stu-id="a61b8-123">Adding Atlassian Cloud from hello gallery</span></span>
<span data-ttu-id="a61b8-124">tooconfigure hello 整合 Atlassian 雲端的 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Atlassian 雲端。</span><span class="sxs-lookup"><span data-stu-id="a61b8-124">tooconfigure hello integration of Atlassian Cloud into Azure AD, you need tooadd Atlassian Cloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a61b8-125">**tooadd Atlassian 雲端 hello 圖庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a61b8-125">**tooadd Atlassian Cloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61b8-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a61b8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a61b8-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a61b8-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="a61b8-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a61b8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="a61b8-133">在 [hello] 搜尋方塊中，輸入**Atlassian 雲端**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-133">In hello search box, type **Atlassian Cloud**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="a61b8-135">在 hello 結果 窗格中，選取  **Atlassian 雲端**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a61b8-135">In hello results panel, select **Atlassian Cloud**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a61b8-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a61b8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a61b8-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Atlassian Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a61b8-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a61b8-139">單一登入 toowork，Azure AD 需要 tooknow Atlassian 雲端中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="a61b8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atlassian Cloud is tooa user in Azure AD.</span></span> <span data-ttu-id="a61b8-140">換句話說，Azure AD 使用者與 hello Atlassian 雲端中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="a61b8-140">In other words, a link relationship between an Azure AD user and hello related user in Atlassian Cloud needs toobe established.</span></span>

<span data-ttu-id="a61b8-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** Atlassian 雲端中。</span><span class="sxs-lookup"><span data-stu-id="a61b8-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="a61b8-142">tooconfigure 和測試 Azure AD 單一登入與 Atlassian 雲端，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="a61b8-142">tooconfigure and test Azure AD single sign-on with Atlassian Cloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a61b8-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="a61b8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a61b8-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="a61b8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a61b8-145">**[建立測試使用者 Atlassian 雲端](#creating-an-atlassian-cloud-test-user)** -toohave 許 Simon Atlassian 雲端是連結的 toohello Azure AD 使用者表示法中對應項目。</span><span class="sxs-lookup"><span data-stu-id="a61b8-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - toohave a counterpart of Britta Simon in Atlassian Cloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a61b8-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a61b8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a61b8-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="a61b8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a61b8-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="a61b8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a61b8-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Atlassian 雲端應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="a61b8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="a61b8-150">**tooconfigure Azure AD 單一登入與 Atlassian 的雲端，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a61b8-150">**tooconfigure Azure AD single sign-on with Atlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61b8-151">在 Azure 入口網站上 hello hello **Atlassian 雲端**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-151">In hello Azure portal, on hello **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="a61b8-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a61b8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="a61b8-155">在 hello **Atlassian 雲端網域和 Url**區段中，執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **IDP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a61b8-155">On hello **Atlassian Cloud Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="a61b8-157">a.</span><span class="sxs-lookup"><span data-stu-id="a61b8-157">a.</span></span> <span data-ttu-id="a61b8-158">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="a61b8-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="a61b8-159">b.</span><span class="sxs-lookup"><span data-stu-id="a61b8-159">b.</span></span> <span data-ttu-id="a61b8-160">在 hello**回覆 URL**文字方塊中，輸入與 URL:`https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="a61b8-160">In hello **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="a61b8-161">請檢查**顯示進階的 URL 設定**並執行下列步驟，如果您想 tooconfigure hello 應用程式中的 hello **SP**初始模式：</span><span class="sxs-lookup"><span data-stu-id="a61b8-161">Check **Show advanced URL settings** and perform hello following step if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="a61b8-163">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="a61b8-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a61b8-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="a61b8-164">These values are not real.</span></span> <span data-ttu-id="a61b8-165">更新這些值與實際的 hello 識別碼和登入 URL。</span><span class="sxs-lookup"><span data-stu-id="a61b8-165">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="a61b8-166">您可以從 Atlassian 雲端 SAML 組態 畫面中，以取得 hello 確切值。</span><span class="sxs-lookup"><span data-stu-id="a61b8-166">You can get hello exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="a61b8-167">在 hello **SAML 簽章憑證**區段中，按一下**Certificate(Base64)**然後儲存您的電腦上的 hello 憑證檔案。</span><span class="sxs-lookup"><span data-stu-id="a61b8-167">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="a61b8-169">在 hello **Atlassian 雲端組態**區段中，按一下**設定 Atlassian 雲端**tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="a61b8-169">On hello **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a61b8-170">複製 hello **SAML 實體識別碼和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="a61b8-170">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="a61b8-172">tooget SSO 設定您的應用程式登入 toohello Atlassian 入口網站使用 hello 系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="a61b8-172">tooget SSO configured for your application, login toohello Atlassian Portal using hello administrator rights.</span></span>

8. <span data-ttu-id="a61b8-173">在左瀏覽的 hello hello 驗證區段中按一下**網域**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-173">In hello Authentication section of hello left navigation click **Domains**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="a61b8-175">a.</span><span class="sxs-lookup"><span data-stu-id="a61b8-175">a.</span></span> <span data-ttu-id="a61b8-176">在 hello 文字方塊中，輸入您的網域名稱，然後按一下**新增網域**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-176">In hello textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="a61b8-178">b.</span><span class="sxs-lookup"><span data-stu-id="a61b8-178">b.</span></span> <span data-ttu-id="a61b8-179">tooverify hello 網域中，按一下 **確認**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-179">tooverify hello domain, click **Verify**.</span></span> 

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="a61b8-181">c.</span><span class="sxs-lookup"><span data-stu-id="a61b8-181">c.</span></span> <span data-ttu-id="a61b8-182">下載 hello 網域驗證 html 檔案，將它上傳您的網域網站 toohello 根資料夾，然後按一下**驗證網域**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-182">Download hello domain verification html file, upload it toohello root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="a61b8-184">d.</span><span class="sxs-lookup"><span data-stu-id="a61b8-184">d.</span></span> <span data-ttu-id="a61b8-185">一旦已驗證網域 hello，hello 值 hello**狀態**欄位是**Verified**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-185">Once hello domain is verified, hello value of hello **Status** field is **Verified**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="a61b8-187">在 hello 左的導覽列中，按一下  **SAML**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-187">In hello left navigation bar, click **SAML**.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="a61b8-189">建立 SAML 設定並新增 hello 身分識別提供者組態。</span><span class="sxs-lookup"><span data-stu-id="a61b8-189">Create a SAML Configuration and add hello Identity provider configuration.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="a61b8-191">a.</span><span class="sxs-lookup"><span data-stu-id="a61b8-191">a.</span></span> <span data-ttu-id="a61b8-192">在 [hello**身分識別提供者實體識別碼**] 文字方塊中，貼上 hello 值**SAML 實體識別碼**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="a61b8-192">In hello **Identity provider Entity ID** text box, paste hello value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a61b8-193">b.</span><span class="sxs-lookup"><span data-stu-id="a61b8-193">b.</span></span> <span data-ttu-id="a61b8-194">在 [hello**身分識別提供者 SSO URL** ] 文字方塊中，貼上 hello 值**SAML 單一登入服務 URL**您從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="a61b8-194">In hello **Identity provider SSO URL** text box, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a61b8-195">c.</span><span class="sxs-lookup"><span data-stu-id="a61b8-195">c.</span></span> <span data-ttu-id="a61b8-196">開啟下載的 hello 憑證從 Azure 入口網站和複製 hello 值而未加以 hello 開始和結束行並將它貼在 hello**公用 X509 憑證**方塊。</span><span class="sxs-lookup"><span data-stu-id="a61b8-196">Open hello downloaded certificate from Azure portal and copy hello values without hello Begin and End lines and paste it in hello **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="a61b8-197">d.</span><span class="sxs-lookup"><span data-stu-id="a61b8-197">d.</span></span> <span data-ttu-id="a61b8-198">按一下**儲存設定**tooSave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="a61b8-198">Click **Save Configuration**  tooSave hello settings.</span></span>
     
11. <span data-ttu-id="a61b8-199">更新 hello Azure AD 設定 toomake 確定您已安裝 hello 更正識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="a61b8-199">Update hello Azure AD settings toomake sure that you have setup hello correct Identifier URL.</span></span>
  
    <span data-ttu-id="a61b8-200">a.</span><span class="sxs-lookup"><span data-stu-id="a61b8-200">a.</span></span> <span data-ttu-id="a61b8-201">複製 hello**預存程序識別 ID** hello SAML 在畫面中，並將它貼在 Azure AD 作為 hello**識別碼**值。</span><span class="sxs-lookup"><span data-stu-id="a61b8-201">Copy hello **SP Identity ID** from hello SAML screen and paste it in Azure AD as hello **Identifier** value.</span></span>

    <span data-ttu-id="a61b8-202">b.</span><span class="sxs-lookup"><span data-stu-id="a61b8-202">b.</span></span> <span data-ttu-id="a61b8-203">登入 URL 是 Atlassian 雲端 hello 租用戶 URL。</span><span class="sxs-lookup"><span data-stu-id="a61b8-203">Sign On URL is hello tenant URL of your Atlassian Cloud.</span></span>     

     ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="a61b8-205">在 hello Azure 入口網站，按一下 **儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a61b8-205">In hello Azure portal, Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="a61b8-207">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="a61b8-207">You can now read a concise version of these instructions inside hello [Azure  portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a61b8-208">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="a61b8-208">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a61b8-209">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a61b8-209">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a61b8-210">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a61b8-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="a61b8-211">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="a61b8-211">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="a61b8-213">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a61b8-213">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61b8-214">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="a61b8-214">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a61b8-216">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-216">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a61b8-218">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="a61b8-218">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a61b8-220">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="a61b8-220">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a61b8-222">a.</span><span class="sxs-lookup"><span data-stu-id="a61b8-222">a.</span></span> <span data-ttu-id="a61b8-223">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-223">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a61b8-224">b.</span><span class="sxs-lookup"><span data-stu-id="a61b8-224">b.</span></span> <span data-ttu-id="a61b8-225">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="a61b8-225">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a61b8-226">c.</span><span class="sxs-lookup"><span data-stu-id="a61b8-226">c.</span></span> <span data-ttu-id="a61b8-227">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-227">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a61b8-228">d.</span><span class="sxs-lookup"><span data-stu-id="a61b8-228">d.</span></span> <span data-ttu-id="a61b8-229">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a61b8-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="a61b8-230">建立 Atlassian Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="a61b8-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="a61b8-231">tooenable Azure AD 使用者 toolog 中 tooAtlassian 雲端，您必須佈建到 Atlassian 雲端。</span><span class="sxs-lookup"><span data-stu-id="a61b8-231">tooenable Azure AD users toolog in tooAtlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="a61b8-232">Atlassian Cloud 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="a61b8-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="a61b8-233">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a61b8-233">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61b8-234">在 hello 站台管理 區段中，按一下 hello**使用者**按鈕</span><span class="sxs-lookup"><span data-stu-id="a61b8-234">In hello Site administration section, click hello **Users** button</span></span>

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="a61b8-236">按一下 hello **Create User**按鈕 toocreate hello Atlassian 雲端中的使用者</span><span class="sxs-lookup"><span data-stu-id="a61b8-236">Click hello **Create User** button toocreate a user in hello Atlassian Cloud</span></span>

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="a61b8-238">輸入 hello 使用者**電子郵件地址**， **Username**，和**全名**及指派 hello 應用程式存取權。</span><span class="sxs-lookup"><span data-stu-id="a61b8-238">Enter hello user's **Email address**, **Username**, and **Full Name** and assign hello application access.</span></span> 

    ![建立 Atlassian Cloud 使用者](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="a61b8-240">按一下**建立使用者**按鈕時，它會傳送 hello 電子郵件邀請 toohello 使用者和之後接受 hello 邀請 hello 使用者將會啟用 hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="a61b8-240">Click **Create user** button, it will send hello email invitation toohello user and after accepting hello invitation hello user will be active in hello system.</span></span> 

>[!NOTE] 
><span data-ttu-id="a61b8-241">您也可以建立 hello 大量使用者按一下 hello**大量建立**hello 使用者 區段中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="a61b8-241">You can also create hello bulk users by clicking hello **Bulk Create** button in hello Users section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a61b8-242">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="a61b8-242">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a61b8-243">在本節中，您可以授與存取 tooAtlassian 雲端啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="a61b8-243">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtlassian Cloud.</span></span>

![指派使用者][200] 

<span data-ttu-id="a61b8-245">**tooassign 許 Simon tooAtlassian 雲端中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="a61b8-245">**tooassign Britta Simon tooAtlassian Cloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="a61b8-246">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-246">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="a61b8-248">在 [hello] 應用程式清單中，選取**Atlassian 雲端**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-248">In hello applications list, select **Atlassian Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="a61b8-250">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="a61b8-250">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="a61b8-252">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a61b8-252">Click **Add** button.</span></span> <span data-ttu-id="a61b8-253">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="a61b8-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="a61b8-255">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="a61b8-255">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a61b8-256">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a61b8-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a61b8-257">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="a61b8-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a61b8-258">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="a61b8-258">Testing single sign-on</span></span>

<span data-ttu-id="a61b8-259">本節中，您可以測試使用存取面板 hello Azure AD 的 SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="a61b8-259">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="a61b8-260">當您按一下的 hello Atlassian 雲端磚 hello 存取面板中時，您應該取得自動登入 tooyour Atlassian 雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="a61b8-260">When you click hello Atlassian Cloud tile in hello Access Panel, you should get automatically signed-on tooyour Atlassian Cloud application.</span></span> <span data-ttu-id="a61b8-261">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="a61b8-261">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a61b8-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="a61b8-262">Additional resources</span></span>

* [<span data-ttu-id="a61b8-263">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a61b8-263">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a61b8-264">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="a61b8-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

