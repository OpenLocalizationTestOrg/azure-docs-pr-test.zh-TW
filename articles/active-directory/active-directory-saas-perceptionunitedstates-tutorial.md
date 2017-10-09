---
title: "教學課程：Azure Active Directory 與 Perception United States (非 UltiPro) 整合 |Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與感覺 United States (非 UltiPro) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="acf7c-103">教學課程：Azure Active Directory 與 Perception United States (非 UltiPro) 整合</span><span class="sxs-lookup"><span data-stu-id="acf7c-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="acf7c-104">在此教學課程中，您學會如何 toointegrate 感覺 United States (非 UltiPro) 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="acf7c-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="acf7c-105">與 Azure AD 整合感覺 United States (非 UltiPro) 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="acf7c-106">您可以控制存取 tooPerception 美國 (非 UltiPro) 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="acf7c-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="acf7c-107">您可以啟用您的使用者 tooautomatically get 登入 tooPerception 美國 (非-UltiPro) （單一登入） 具有其 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="acf7c-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="acf7c-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="acf7c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="acf7c-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="acf7c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acf7c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="acf7c-110">Prerequisites</span></span>

<span data-ttu-id="acf7c-111">tooconfigure Azure AD 整合與感覺 United States (非 UltiPro)，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="acf7c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="acf7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="acf7c-113">已啟用 Perception United States (非 UltiPro) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="acf7c-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="acf7c-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="acf7c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="acf7c-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="acf7c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="acf7c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="acf7c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="acf7c-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="acf7c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="acf7c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="acf7c-118">Scenario description</span></span>
<span data-ttu-id="acf7c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acf7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="acf7c-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="acf7c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="acf7c-121">從 hello 圖庫加入感覺 United States (非 UltiPro)</span><span class="sxs-lookup"><span data-stu-id="acf7c-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="acf7c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="acf7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="acf7c-123">從 hello 圖庫加入感覺 United States (非 UltiPro)</span><span class="sxs-lookup"><span data-stu-id="acf7c-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="acf7c-124">tooconfigure hello 整合的感覺 United States (非 UltiPro) 至 Azure AD，您會需要 tooadd 感覺 United States (非 UltiPro) 從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單。</span><span class="sxs-lookup"><span data-stu-id="acf7c-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="acf7c-125">**tooadd 感覺 United States (非 UltiPro) 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acf7c-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf7c-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="acf7c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="acf7c-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="acf7c-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="acf7c-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="acf7c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="acf7c-133">在 hello 搜尋方塊中，輸入**感覺 United States (非 UltiPro)**，選取**感覺 United States (非 UltiPro)**然後按一下 從結果面板**新增**按鈕 tooaddhello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acf7c-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Hello 結果清單中的感覺 United States (非 UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="acf7c-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="acf7c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="acf7c-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Perception United States (非 UltiPro) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acf7c-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="acf7c-137">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中感覺 United States (非 UltiPro) 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="acf7c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="acf7c-138">換句話說，Azure AD 使用者與 hello 相關的使用者的感覺 United States (非 UltiPro) 之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="acf7c-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="acf7c-139">在感覺 United States (非 UltiPro)，將指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="acf7c-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="acf7c-140">tooconfigure 和測試 Azure AD 單一登入與感覺 United States (非 UltiPro)，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="acf7c-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="acf7c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="acf7c-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="acf7c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="acf7c-143">**[建立感覺 United States (非 UltiPro) 測試使用者](#create-a-perception-united-states-non-ultipro-test-user)** -toohave 許 Simon 中感覺 United States (非 UltiPro) 表示法連結的 toohello Azure AD 使用者的對應項目。</span><span class="sxs-lookup"><span data-stu-id="acf7c-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="acf7c-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acf7c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="acf7c-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="acf7c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="acf7c-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="acf7c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="acf7c-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並感覺 United States (非 UltiPro) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="acf7c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="acf7c-148">**tooconfigure Azure AD 單一登入與感覺 United States (非-UltiPro)，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acf7c-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="acf7c-149">在 Azure 入口網站上 hello hello**感覺 United States (非 UltiPro)**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="acf7c-151">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="acf7c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="acf7c-153">在 hello**感覺 United States (非 UltiPro) 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Perception United States (非 UltiPro) 網域與 URL 單一登入資訊](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="acf7c-155">a.</span><span class="sxs-lookup"><span data-stu-id="acf7c-155">a.</span></span> <span data-ttu-id="acf7c-156">在 hello**識別碼**文字方塊中，型別 hello URL:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="acf7c-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="acf7c-157">b.</span><span class="sxs-lookup"><span data-stu-id="acf7c-157">b.</span></span> <span data-ttu-id="acf7c-158">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="acf7c-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="acf7c-159">hello 值不是真正的。</span><span class="sxs-lookup"><span data-stu-id="acf7c-159">hello value is not real.</span></span> <span data-ttu-id="acf7c-160">您將會更新 hello 實際回覆 URL，在 hello 教學課程稍後會說明 hello 值。</span><span class="sxs-lookup"><span data-stu-id="acf7c-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="acf7c-161">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="acf7c-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="acf7c-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="acf7c-163">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="acf7c-165">在 hello**感覺 United States (非 UltiPro) 組態**區段中，按一下**設定感覺 United States (非 UltiPro)** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="acf7c-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="acf7c-166">複製 hello **SAML 實體識別碼**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="acf7c-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="acf7c-167">a.</span><span class="sxs-lookup"><span data-stu-id="acf7c-167">a.</span></span> <span data-ttu-id="acf7c-168">hello**感覺 United States (非 UltiPro)**應用程式需要 hello **SAML 實體識別碼**值，您已複製，toobe uri 編碼。</span><span class="sxs-lookup"><span data-stu-id="acf7c-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="acf7c-169">tooget hello 編碼的 uri 值，使用 hello 以下連結：**http://www.url-encode-decode.com/**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="acf7c-170">b.</span><span class="sxs-lookup"><span data-stu-id="acf7c-170">b.</span></span> <span data-ttu-id="acf7c-171">取得 hello uri 之後編碼的值將其與 hello**回覆 URL**如所述的以下層</span><span class="sxs-lookup"><span data-stu-id="acf7c-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="acf7c-172">c.</span><span class="sxs-lookup"><span data-stu-id="acf7c-172">c.</span></span> <span data-ttu-id="acf7c-173">貼上 hello hello 中的值之上**回覆 URL**  文字方塊中的**感覺 United States (非 UltiPro) 網域和 Url** > 一節。</span><span class="sxs-lookup"><span data-stu-id="acf7c-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Perception United States (非 UltiPro) 設定](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="acf7c-175">在另一個瀏覽器視窗中，系統管理員身分登入 tooyour 感覺 United States (非 UltiPro) 公司網站。</span><span class="sxs-lookup"><span data-stu-id="acf7c-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="acf7c-176">在 hello 主要工具列上，按一下 **帳戶設定**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Perception United States (非 UltiPro) 使用者](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="acf7c-178">在 hello**帳戶設定**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Perception United States (非 UltiPro) 使用者](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="acf7c-180">a.</span><span class="sxs-lookup"><span data-stu-id="acf7c-180">a.</span></span> <span data-ttu-id="acf7c-181">在 hello**公司名稱**文字方塊中，型別 hello 名稱 hello**公司**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="acf7c-182">b.</span><span class="sxs-lookup"><span data-stu-id="acf7c-182">b.</span></span> <span data-ttu-id="acf7c-183">在 hello**帳戶名稱**文字方塊中，型別 hello 名稱 hello**帳戶**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="acf7c-184">c.</span><span class="sxs-lookup"><span data-stu-id="acf7c-184">c.</span></span> <span data-ttu-id="acf7c-185">在**預設回覆 tooEmail**文字方塊中，有效的型別 hello**電子郵件**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="acf7c-186">d.</span><span class="sxs-lookup"><span data-stu-id="acf7c-186">d.</span></span> <span data-ttu-id="acf7c-187">為 [SSO 識別提供者] 選取 [SAML 2.0]。</span><span class="sxs-lookup"><span data-stu-id="acf7c-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="acf7c-188">在 hello **SSO 組態**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![Perception United States (非 UltiPro) SSOConfig](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="acf7c-190">a.</span><span class="sxs-lookup"><span data-stu-id="acf7c-190">a.</span></span> <span data-ttu-id="acf7c-191">為 [SAML NameID 類型] 選取 [電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="acf7c-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="acf7c-192">b.</span><span class="sxs-lookup"><span data-stu-id="acf7c-192">b.</span></span> <span data-ttu-id="acf7c-193">在 hello **SSO 組態名稱**文字方塊中，型別名稱 hello 您**組態**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="acf7c-194">c.</span><span class="sxs-lookup"><span data-stu-id="acf7c-194">c.</span></span> <span data-ttu-id="acf7c-195">在**身分識別提供者名稱**文字方塊中，貼上 hello 值**SAML 實體識別碼**，從 Azure 入口網站複製的。</span><span class="sxs-lookup"><span data-stu-id="acf7c-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="acf7c-196">d.</span><span class="sxs-lookup"><span data-stu-id="acf7c-196">d.</span></span> <span data-ttu-id="acf7c-197">在**SAML 網域文字方塊**，輸入 hello 網域，像是 **@contoso.com** 。</span><span class="sxs-lookup"><span data-stu-id="acf7c-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="acf7c-198">e.</span><span class="sxs-lookup"><span data-stu-id="acf7c-198">e.</span></span> <span data-ttu-id="acf7c-199">按一下**再次上傳**tooupload hello**中繼資料 XML**檔案。</span><span class="sxs-lookup"><span data-stu-id="acf7c-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="acf7c-200">f.</span><span class="sxs-lookup"><span data-stu-id="acf7c-200">f.</span></span> <span data-ttu-id="acf7c-201">按一下 [更新] 。</span><span class="sxs-lookup"><span data-stu-id="acf7c-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="acf7c-202">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="acf7c-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="acf7c-203">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="acf7c-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="acf7c-204">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="acf7c-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="acf7c-205">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="acf7c-205">Create an Azure AD test user</span></span>

<span data-ttu-id="acf7c-206">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="acf7c-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="acf7c-208">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acf7c-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="acf7c-209">在 hello Azure 入口網站，hello 左窗格中，按一下 hello **Azure Active Directory**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="acf7c-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="acf7c-211">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="acf7c-213">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="acf7c-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![hello [新增] 按鈕](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="acf7c-215">在 hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="acf7c-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![hello [使用者] 對話方塊](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="acf7c-217">a.</span><span class="sxs-lookup"><span data-stu-id="acf7c-217">a.</span></span> <span data-ttu-id="acf7c-218">在 hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="acf7c-219">b.</span><span class="sxs-lookup"><span data-stu-id="acf7c-219">b.</span></span> <span data-ttu-id="acf7c-220">在 hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="acf7c-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="acf7c-221">c.</span><span class="sxs-lookup"><span data-stu-id="acf7c-221">c.</span></span> <span data-ttu-id="acf7c-222">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="acf7c-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="acf7c-223">d.</span><span class="sxs-lookup"><span data-stu-id="acf7c-223">d.</span></span> <span data-ttu-id="acf7c-224">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="acf7c-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="acf7c-225">建立 Perception United States (非 UltiPro) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="acf7c-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="acf7c-226">在本節中，您會於 Perception United States (非 UltiPro) 建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="acf7c-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="acf7c-227">使用[感覺 United States (非 UltiPro) 支援小組](http://www.ultimatesoftware.com/Contact/ContactUs)tooadd hello hello 感覺 United States (非 UltiPro) 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="acf7c-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="acf7c-228">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="acf7c-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="acf7c-229">在本節中，以啟用許 Simon toouse Azure 單一登入授與存取 tooPerception 美國 (非 UltiPro)。</span><span class="sxs-lookup"><span data-stu-id="acf7c-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="acf7c-231">**tooassign 許 Simon tooPerception 美國 (非-UltiPro)，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="acf7c-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="acf7c-232">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="acf7c-234">在 [hello] 應用程式清單中，選取**感覺 United States (非 UltiPro)**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![hello 應用程式清單中的 hello 感覺 United States (非 UltiPro) 連結](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="acf7c-236">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="acf7c-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="acf7c-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acf7c-238">Click **Add** button.</span></span> <span data-ttu-id="acf7c-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="acf7c-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="acf7c-241">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="acf7c-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="acf7c-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acf7c-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="acf7c-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="acf7c-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="acf7c-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="acf7c-244">Test single sign-on</span></span>

<span data-ttu-id="acf7c-245">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="acf7c-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="acf7c-246">當您按一下 hello 感覺 United States (非 UltiPro) 磚 hello 存取面板中的時，您應該取得自動登入 tooyour 感覺 United States (非 UltiPro) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="acf7c-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="acf7c-247">如需有關存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="acf7c-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="acf7c-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="acf7c-248">Additional resources</span></span>

* [<span data-ttu-id="acf7c-249">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="acf7c-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="acf7c-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="acf7c-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

