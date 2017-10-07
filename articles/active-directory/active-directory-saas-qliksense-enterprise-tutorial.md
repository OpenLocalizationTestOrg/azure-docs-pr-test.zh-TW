---
title: "教學課程：Azure Active Directory 與 Qlik Sense Enterprise 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Qlik 意義企業之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="0d5d7-103">教學課程：Azure Active Directory 與 Qlik Sense Enterprise 整合</span><span class="sxs-lookup"><span data-stu-id="0d5d7-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="0d5d7-104">在此教學課程中，您學會如何 toointegrate Qlik 意義企業與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d5d7-105">與 Azure AD 整合 Qlik 意義 Enterprise 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="0d5d7-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0d5d7-106">您可以控制存取 tooQlik 意義 Enterprise 的 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="0d5d7-107">您可以啟用您的使用者 tooautomatically get 登入 tooQlik （單一登入） 的意義上企業與他們的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="0d5d7-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="0d5d7-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d5d7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d5d7-110">Prerequisites</span></span>

<span data-ttu-id="0d5d7-111">tooconfigure Qlik 意義企業與 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="0d5d7-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="0d5d7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0d5d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d5d7-113">已啟用 Qlik Sense Enterprise 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0d5d7-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d5d7-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d5d7-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0d5d7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d5d7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d5d7-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d5d7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0d5d7-118">Scenario description</span></span>
<span data-ttu-id="0d5d7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d5d7-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0d5d7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d5d7-121">從 hello 圖庫加入 Qlik 意義 Enterprise</span><span class="sxs-lookup"><span data-stu-id="0d5d7-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="0d5d7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0d5d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="0d5d7-123">從 hello 圖庫加入 Qlik 意義 Enterprise</span><span class="sxs-lookup"><span data-stu-id="0d5d7-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="0d5d7-124">tooconfigure hello 整合 Qlik 意義企業到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Qlik 意義企業。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0d5d7-125">**tooadd Qlik 意義企業 hello 圖庫中，從執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0d5d7-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d5d7-126">在 [hello ** [Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="0d5d7-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0d5d7-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-129">Then go too**All applications**.</span></span>

    ![hello 企業應用程式] 刀鋒視窗][2]
    
3. <span data-ttu-id="0d5d7-131">tooadd 新應用程式中，按一下 [**新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="0d5d7-133">在 hello 搜尋方塊中，輸入**Qlik 意義企業**，選取**Qlik 意義企業**然後按一下 [從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Qlik hello [結果] 清單中的意義上企業](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0d5d7-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0d5d7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0d5d7-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Qlik Sense Enterprise 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d5d7-137">單一登入 toowork，Azure AD 需要 tooknow Qlik 意義企業中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="0d5d7-138">換句話說，Azure AD 使用者與 hello Qlik 意義企業中的相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="0d5d7-139">在 Qlik 意義 Enterprise 中，指派 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0d5d7-140">tooconfigure 及 Qlik 意義企業與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="0d5d7-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0d5d7-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0d5d7-142">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d5d7-143">**[建立測試使用者 Qlik 意義企業](#create-a-qlik-sense-enterprise-test-user)** -toohave 許 Simon Qlik 是連結的 toohello Azure AD 使用者表示的意義上企業中的對應項目。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d5d7-144">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d5d7-145">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0d5d7-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0d5d7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0d5d7-147">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 Qlik 意義企業應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="0d5d7-148">**Qlik 意義企業，使用 Azure AD 單一登入 tooconfigure 執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d5d7-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d5d7-149">在 Azure 入口網站上 hello hello **Qlik 意義企業**應用程式整合頁面上，按一下 [**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="0d5d7-151">在 [hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="0d5d7-153">在 [hello **Qlik 意義企業網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d5d7-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Qlik Sense Enterprise 網域與 URL 單一登入資訊](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="0d5d7-155">a.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-155">a.</span></span> <span data-ttu-id="0d5d7-156">在 [hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="0d5d7-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0d5d7-157">請注意結尾的斜線結尾 hello 這個 URI 的 hello。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="0d5d7-158">這是必要的。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-158">It is required.</span></span>
    
    <span data-ttu-id="0d5d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-159">b.</span></span> <span data-ttu-id="0d5d7-160">在 [hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d5d7-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="0d5d7-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-161">These values are not real.</span></span> <span data-ttu-id="0d5d7-162">這些值與 hello 實際登入 URL 和識別碼，稍後在本教學課程中或連絡所說明的更新[Qlik 意義企業用戶端支援小組](https://www.qlik.com/us/services/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="0d5d7-163">在 [hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="0d5d7-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-165">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d5d7-167">準備 hello 同盟中繼資料 XML 檔案，以便您可以上傳該 tooQlik 意義上伺服器。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="0d5d7-168">上傳之前 hello IdP 中繼資料 toohello Qlik 意義伺服器，hello 檔案需要編輯 toobe tooremove 資訊 tooensure 正常運作之間 Azure AD 和 Qlik 意義上伺服器。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="0d5d7-170">a.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-170">a.</span></span> <span data-ttu-id="0d5d7-171">開啟 hello FederationMetaData.xml 檔案，從文字編輯器中的 Azure 入口網站下載。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="0d5d7-172">b.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-172">b.</span></span> <span data-ttu-id="0d5d7-173">搜尋的 hello value **RoleDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="0d5d7-174">共會有四個項目 (兩對開頭和結尾元素標籤)。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="0d5d7-175">c.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-175">c.</span></span> <span data-ttu-id="0d5d7-176">從 hello 檔案之間刪除 hello RoleDescriptor 標記和所有資訊。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="0d5d7-177">d.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-177">d.</span></span> <span data-ttu-id="0d5d7-178">儲存 hello 檔案，並將它附近保留供稍後在這份文件中使用。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="0d5d7-179">瀏覽 toohello Qlik 意義 Qlik 管理主控台 (QMC)，使用者可以建立虛擬 proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="0d5d7-180">在 [hello QMC，按一下 hello**虛擬 Proxy**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="0d5d7-182">在 hello 囉 」 畫面底部，按一下 [hello**建立新**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="0d5d7-184">hello 虛擬 proxy 編輯畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="0d5d7-185">Hello hello 螢幕的右邊是顯示組態選項的功能表。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="0d5d7-187">檢查 hello 識別功能表選項，輸入 hello hello Azure 的虛擬 proxy 組態的識別資訊。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="0d5d7-189">a.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-189">a.</span></span> <span data-ttu-id="0d5d7-190">hello**描述**欄位是 hello 虛擬 proxy 組態的易記名稱。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="0d5d7-191">輸入說明的值。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="0d5d7-192">b.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-192">b.</span></span> <span data-ttu-id="0d5d7-193">hello**首碼**欄位識別 hello 虛擬 proxy 端點連接 tooQlik 意義上與 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="0d5d7-194">輸入此虛擬 Proxy 的獨特前置詞名稱。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="0d5d7-195">c.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-195">c.</span></span> <span data-ttu-id="0d5d7-196">**工作階段閒置逾時 （分鐘）** hello 逾時，透過此虛擬 proxy 的連線。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="0d5d7-197">d.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-197">d.</span></span> <span data-ttu-id="0d5d7-198">hello**工作階段 cookie 標頭名稱**是 hello cookie 名稱儲存 hello 的 hello Qlik 意義上，使用者的工作階段收到驗證成功後的工作階段識別項。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="0d5d7-199">此名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-199">This name must be unique.</span></span>

12. <span data-ttu-id="0d5d7-200">按一下 hello 驗證功能表選項 toomake 看到它。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="0d5d7-201">hello 驗證畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="0d5d7-203">a.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-203">a.</span></span> <span data-ttu-id="0d5d7-204">hello**匿名存取模式**下拉式清單決定匿名使用者可能會透過 hello 虛擬 proxy 存取 Qlik 意義。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="0d5d7-205">hello 預設選項為匿名使用者。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="0d5d7-206">b.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-206">b.</span></span> <span data-ttu-id="0d5d7-207">hello**驗證方法**下拉式清單可讓您決定要使用 hello 驗證配置 hello 虛擬 proxy。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="0d5d7-208">選取 [SAML hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="0d5d7-209">此時會顯示更多選項。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="0d5d7-210">c.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-210">c.</span></span> <span data-ttu-id="0d5d7-211">在 [hello **SAML 主機 URI 欄位**，輸入的 hello 主機名稱的使用者輸入 tooaccess Qlik 意義上的，透過這個 SAML 虛擬 proxy。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="0d5d7-212">hello 主機名稱為 hello Qlik 意義伺服器 hello uri。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="0d5d7-213">d.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-213">d.</span></span> <span data-ttu-id="0d5d7-214">在 [hello **SAML 實體識別碼**，輸入的 hello hello SAML 主機 URI 欄位中輸入相同的值。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="0d5d7-215">e.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-215">e.</span></span> <span data-ttu-id="0d5d7-216">hello **SAML Ldp 中繼資料**是稍早在 hello 中編輯 hello 檔案**編輯同盟中繼資料從 Azure AD 設定**> 一節。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="0d5d7-217">**上傳之前 hello IdP 中繼資料，hello 檔案需要編輯 toobe** Azure AD 之間的 tooremove 資訊 tooensure 正常運作和 Qlik 意義上伺服器。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="0d5d7-218">**請如果 hello 檔案有尚未 toobe 編輯，參閱上述的 toohello 指示。**</span><span class="sxs-lookup"><span data-stu-id="0d5d7-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="0d5d7-219">如果已編輯 hello 檔案按一下 hello 瀏覽按鈕並選取 hello 編輯過的中繼資料檔案 tooupload 它 toohello 虛擬的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="0d5d7-220">f.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-220">f.</span></span> <span data-ttu-id="0d5d7-221">輸入代表 hello hello SAML 屬性 hello 屬性名稱或結構描述參照**UserID** Azure AD 會傳送 toohello Qlik 意義上伺服器。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="0d5d7-222">提供設定 hello Azure 應用程式的螢幕前結構描述參考資訊。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="0d5d7-223">toouse hello name 屬性，輸入`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="0d5d7-224">g.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-224">g.</span></span> <span data-ttu-id="0d5d7-225">輸入 hello hello 值**使用者目錄**tooQlik 意義伺服器透過 Azure AD 驗證時，這會是附加的 toousers。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="0d5d7-226">硬式編碼值必須以**方括號 []** 括住。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="0d5d7-227">toouse 屬性傳送 hello Azure AD SAML 判斷提示，在此文字方塊中輸入 hello 屬性名稱的 hello**沒有**方括號。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="0d5d7-228">h.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-228">h.</span></span> <span data-ttu-id="0d5d7-229">hello **SAML 簽章演算法**集 hello 服務提供者 （在此案例的 Qlik 意義伺服器） 的憑證簽署 hello 虛擬的 proxy 設定。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="0d5d7-230">如果 Qlik 意義伺服器使用信任的憑證，使用 Microsoft Enhanced RSA 與 AES 密碼編譯提供者所產生，變更 hello SAML 簽章演算法太**sha-256**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="0d5d7-231">i.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-231">i.</span></span> <span data-ttu-id="0d5d7-232">hello SAML 屬性的對應區段可讓您在安全性規則中使用的群組傳送 toobe tooQlik 意義之類的其他屬性。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="0d5d7-233">按一下 hello**負載平衡**功能表選項 toomake 看到它。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="0d5d7-234">hello 負載平衡畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="0d5d7-236">按一下 hello**新增新的伺服器節點**按鈕，選取引擎] 節點或節點 Qlik 意義上會傳送工作階段 toofor 負載平衡的目的，然後按一下 [hello**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="0d5d7-238">按一下 hello 進階] 功能表選項 toomake 看到它。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="0d5d7-239">hello 進階的畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="0d5d7-241">hello 主機白名單識別時連接 toohello Qlik 意義伺服器可接受的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="0d5d7-242">**輸入 hello tooQlik 意義伺服器連線時，使用者將指定的主機名稱。**</span><span class="sxs-lookup"><span data-stu-id="0d5d7-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="0d5d7-243">hello 主機名稱為 hello 相同的值為 hello hello https:// 沒有 SAML 主機 uri。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="0d5d7-244">按一下 hello**套用**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="0d5d7-246">按一下 [確定] tooaccept hello 警告訊息，指出將會重新啟動連結的 toohello 虛擬 proxy 的 proxy。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="0d5d7-248">右側 hello 囉 」 畫面，hello 相關聯的項目功能表隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="0d5d7-249">按一下 hello **Proxy**功能表選項。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="0d5d7-251">hello proxy 畫面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-251">hello proxy screen appears.</span></span>  <span data-ttu-id="0d5d7-252">按一下 hello**連結**按鈕 hello 底部 toolink proxy toohello 虛擬 proxy。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="0d5d7-254">選取 hello proxy 節點，將會支援此虛擬 proxy 連線並按一下 hello**連結**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="0d5d7-255">之後連結，hello proxy 會列在相關聯 proxy。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="0d5d7-258">後約五 tooten 秒 hello 重新整理 QMC 訊息會出現。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="0d5d7-259">按一下 hello**重新整理 QMC** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="0d5d7-261">當 hello QMC 重新整理時，按一下以 hello**虛擬 proxy**功能表項目。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="0d5d7-262">hello 新 SAML 虛擬 proxy 的項目會列在 hello 囉 」 畫面上的資料表。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="0d5d7-263">只要在 hello 虛擬 proxy 項目上按一下。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="0d5d7-265">在 hello 囉 」 畫面底部，將會啟動 hello 下載 SP 中繼資料] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="0d5d7-266">按一下 hello**下載 SP 中繼資料**按鈕 toosave hello 中繼資料 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="0d5d7-268">開啟 hello sp 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="0d5d7-269">觀察 hello **entityID**項目和 hello **AssertionConsumerService**項目。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="0d5d7-270">這些值是對等 toohello**識別碼**和 hello**登入 URL** hello Azure AD 應用程式組態中。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="0d5d7-271">將這些值貼入中 hello **Qlik 意義企業網域和 Url**如果它們不相符，則您應該將它們取代 hello Azure AD 應用程式組態精靈中的 hello Azure AD 的應用程式組態中的區段。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="0d5d7-273">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="0d5d7-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0d5d7-274">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入**] 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0d5d7-275">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0d5d7-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0d5d7-276">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0d5d7-276">Create an Azure AD test user</span></span>
<span data-ttu-id="0d5d7-277">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="0d5d7-279">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="0d5d7-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d5d7-280">在 [hello Azure 入口網站，hello 左窗格中，按一下 [hello **Azure Active Directory** ] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![hello Azure Active Directory] 按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0d5d7-282">toodisplay hello 使用者清單，請移過**使用者和群組**，然後按一下 [**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0d5d7-284">tooopen hello**使用者**對話方塊中，按一下 [**新增**頂端的 hello hello**所有使用者**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![hello [新增] 按鈕](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0d5d7-286">在 [hello**使用者**對話方塊方塊中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d5d7-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![hello [使用者] 對話方塊](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="0d5d7-288">a.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-288">a.</span></span> <span data-ttu-id="0d5d7-289">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="0d5d7-290">b.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-290">b.</span></span> <span data-ttu-id="0d5d7-291">在 [hello**使用者名**方塊中，使用者許 Simon 類型 hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="0d5d7-292">c.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-292">c.</span></span> <span data-ttu-id="0d5d7-293">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="0d5d7-294">d.</span><span class="sxs-lookup"><span data-stu-id="0d5d7-294">d.</span></span> <span data-ttu-id="0d5d7-295">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="0d5d7-296">建立 Qlik Sense Enterprise 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0d5d7-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="0d5d7-297">在本節中，您要在 Qlik Sense Enterprise 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="0d5d7-298">使用[Qlik 意義企業用戶端支援小組](https://www.qlik.com/us/services/support)hello Qlik 意義企業平台中新增 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="0d5d7-299">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0d5d7-300">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0d5d7-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0d5d7-301">在本節中，您可以授與存取 tooQlik 意義企業啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![指派 hello 使用者角色][200] 

<span data-ttu-id="0d5d7-303">**tooassign 許 Simon tooQlik 意義企業執行 hello 下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0d5d7-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="0d5d7-304">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 [**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0d5d7-306">在 [hello] 應用程式清單中，選取**Qlik 意義企業**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![hello 應用程式清單中的 hello Qlik 意義企業連結](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="0d5d7-308">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202]

4. <span data-ttu-id="0d5d7-310">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-310">Click **Add** button.</span></span> <span data-ttu-id="0d5d7-311">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="0d5d7-313">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者] 清單中。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0d5d7-314">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d5d7-315">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0d5d7-316">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0d5d7-316">Test single sign-on</span></span>

<span data-ttu-id="0d5d7-317">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0d5d7-318">當您按一下 hello Qlik 意義企業磚 hello 存取面板中的時，您應該取得自動登入 tooyour Qlik 意義企業應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d5d7-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="0d5d7-319">其他資源</span><span class="sxs-lookup"><span data-stu-id="0d5d7-319">Additional resources</span></span>

* [<span data-ttu-id="0d5d7-320">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d5d7-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d5d7-321">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0d5d7-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

