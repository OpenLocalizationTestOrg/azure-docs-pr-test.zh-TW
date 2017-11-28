---
title: "教學課程：Azure Active Directory 與 Absorb LMS 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 和吸收 LMS 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a><span data-ttu-id="1276a-103">教學課程：Azure Active Directory 與 Absorb LMS</span><span class="sxs-lookup"><span data-stu-id="1276a-103">Tutorial: Azure Active Directory integration with Absorb LMS</span></span>

<span data-ttu-id="1276a-104">在此教學課程中，您學會如何 toointegrate Absorb LMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1276a-104">In this tutorial, you learn how toointegrate Absorb LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1276a-105">吸收 LMS 整合與 Azure AD 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-105">Integrating Absorb LMS with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1276a-106">您可以控制存取 tooAbsorb LMS Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="1276a-106">You can control in Azure AD who has access tooAbsorb LMS</span></span>
- <span data-ttu-id="1276a-107">您可以啟用您的使用者 tooautomatically get 登入 tooAbsorb LMS （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="1276a-107">You can enable your users tooautomatically get signed-on tooAbsorb LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1276a-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="1276a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1276a-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱。</span><span class="sxs-lookup"><span data-stu-id="1276a-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="1276a-110">[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1276a-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1276a-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="1276a-111">Prerequisites</span></span>

<span data-ttu-id="1276a-112">tooconfigure Azure AD 與吸收 LMS 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-112">tooconfigure Azure AD integration with Absorb LMS, you need hello following items:</span></span>

- <span data-ttu-id="1276a-113">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1276a-113">An Azure AD subscription</span></span>
- <span data-ttu-id="1276a-114">已啟用 Absorb LMS 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1276a-114">An Absorb LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1276a-115">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="1276a-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1276a-116">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1276a-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1276a-117">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1276a-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1276a-118">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1276a-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1276a-119">案例描述</span><span class="sxs-lookup"><span data-stu-id="1276a-119">Scenario description</span></span>
<span data-ttu-id="1276a-120">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1276a-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1276a-121">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="1276a-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1276a-122">從 hello 圖庫加入吸收 LMS</span><span class="sxs-lookup"><span data-stu-id="1276a-122">Adding Absorb LMS from hello gallery</span></span>
2. <span data-ttu-id="1276a-123">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1276a-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-absorb-lms-from-hello-gallery"></a><span data-ttu-id="1276a-124">從 hello 圖庫加入吸收 LMS</span><span class="sxs-lookup"><span data-stu-id="1276a-124">Adding Absorb LMS from hello gallery</span></span>
<span data-ttu-id="1276a-125">tooconfigure hello 整合吸收 LMS tooAzure AD 中的，您需要 tooadd Absorb LMS hello 圖庫 tooyour 清單中的受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1276a-125">tooconfigure hello integration of Absorb LMS in tooAzure AD, you need tooadd Absorb LMS from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1276a-126">**tooadd Absorb LMS 從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1276a-126">**tooadd Absorb LMS from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1276a-127">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1276a-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![hello Azure Active Directory 按鈕][1]

2. <span data-ttu-id="1276a-129">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1276a-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1276a-130">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1276a-130">Then go too**All applications**.</span></span>

    ![hello 企業應用程式 刀鋒視窗][2]
    
3. <span data-ttu-id="1276a-132">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="1276a-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="1276a-134">在 hello 搜尋方塊中，輸入**吸收 LMS**，選取**吸收 LMS**然後按一下 從結果面板**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1276a-134">In hello search box, type **Absorb LMS**, select **Absorb LMS** from result panel then click **Add** button tooadd hello application.</span></span>

    ![吸收 LMS hello [結果] 清單中](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="1276a-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1276a-136">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="1276a-137">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Absorb LMS 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1276a-137">In this section, you configure and test Azure AD single sign-on with Absorb LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1276a-138">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中吸收 LMS 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="1276a-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Absorb LMS is tooa user in Azure AD.</span></span> <span data-ttu-id="1276a-139">換句話說，Azure AD 使用者與 hello 吸收 LMS 中相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="1276a-139">In other words, a link relationship between an Azure AD user and hello related user in Absorb LMS needs toobe established.</span></span>

<span data-ttu-id="1276a-140">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**吸收 LMS 中。</span><span class="sxs-lookup"><span data-stu-id="1276a-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Absorb LMS.</span></span>

<span data-ttu-id="1276a-141">tooconfigure 及吸收 LMS 與 Azure AD 單一登入的測試，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-141">tooconfigure and test Azure AD single sign-on with Absorb LMS, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1276a-142">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="1276a-142">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1276a-143">**[建立 Azure AD 的測試使用者](#create-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1276a-143">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1276a-144">**[建立測試使用者吸收 LMS](#create-an-absorb-lms-test-user)**  -toohave 許 Simon 是連結的 toohello Azure AD 使用者表示吸收 LMS 中對應項目。</span><span class="sxs-lookup"><span data-stu-id="1276a-144">**[Create an Absorb LMS test user](#create-an-absorb-lms-test-user)** - toohave a counterpart of Britta Simon in Absorb LMS that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1276a-145">**[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1276a-145">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1276a-146">**[測試單一登入](#test-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="1276a-146">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="1276a-147">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1276a-147">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="1276a-148">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並吸收 LMS 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1276a-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Absorb LMS application.</span></span>

<span data-ttu-id="1276a-149">**tooconfigure Azure AD 單一登入與吸收 LMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1276a-149">**tooconfigure Azure AD single sign-on with Absorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="1276a-150">在 Azure 入口網站上 hello hello**吸收 LMS**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="1276a-150">In hello Azure portal, on hello **Absorb LMS** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="1276a-152">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1276a-152">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. <span data-ttu-id="1276a-154">在 hello**吸收 LMS 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-154">On hello **Absorb LMS Domain and URLs** section, perform hello following steps:</span></span>

    ![Absorb LMS 網域與 URL 單一登入資訊](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    <span data-ttu-id="1276a-156">a.</span><span class="sxs-lookup"><span data-stu-id="1276a-156">a.</span></span> <span data-ttu-id="1276a-157">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="1276a-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>

    <span data-ttu-id="1276a-158">b.</span><span class="sxs-lookup"><span data-stu-id="1276a-158">b.</span></span> <span data-ttu-id="1276a-159">在 hello**回覆 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<subdomain>.myabsorb.com/Account/SAML`</span><span class="sxs-lookup"><span data-stu-id="1276a-159">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<subdomain>.myabsorb.com/Account/SAML`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="1276a-160">這些值不是真正的 hello。</span><span class="sxs-lookup"><span data-stu-id="1276a-160">These values are not hello real.</span></span> <span data-ttu-id="1276a-161">以 hello 實際的識別項和回覆 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="1276a-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="1276a-162">請連絡[吸收 LMS 用戶端支援小組](https://www.absorblms.com/support)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="1276a-162">Contact [Absorb LMS Client support team](https://www.absorblms.com/support) tooget these values.</span></span> 

4. <span data-ttu-id="1276a-163">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="1276a-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![hello 憑證下載連結](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. <span data-ttu-id="1276a-165">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1276a-165">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="1276a-167">在 hello**吸收 LMS 組態**區段中，按一下**設定吸收 LMS** tooopen**設定登入**視窗。</span><span class="sxs-lookup"><span data-stu-id="1276a-167">On hello **Absorb LMS Configuration** section, click **Configure Absorb LMS** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1276a-168">複製 hello**登出 URL 和 SAML 單一登入服務 URL**從 hello**快速參考 > 一節。**</span><span class="sxs-lookup"><span data-stu-id="1276a-168">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Absorb LMS 設定](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. <span data-ttu-id="1276a-170">在不同的網頁瀏覽器視窗中，系統管理員身分登入 tooyour 吸收 LMS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1276a-170">In a different web browser window, log in tooyour Absorb LMS company site as an administrator.</span></span>

9. <span data-ttu-id="1276a-171">按一下 hello**帳戶圖示**hello 管理介面上。</span><span class="sxs-lookup"><span data-stu-id="1276a-171">Click hello **Account Icon** on hello admin interface.</span></span> 

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/1.png)

10. <span data-ttu-id="1276a-173">按一下 [入口網站設定]。</span><span class="sxs-lookup"><span data-stu-id="1276a-173">Click **Portal Settings**.</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. <span data-ttu-id="1276a-175">按一下 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1276a-175">Click hello **Users** tab.</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/3.png)

12. <span data-ttu-id="1276a-177">執行下列步驟 tooaccess hello 單一登入設定欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-177">Perform hello following steps tooaccess hello Single Sign-On configuration fields:</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/4.png)

    <span data-ttu-id="1276a-179">a.</span><span class="sxs-lookup"><span data-stu-id="1276a-179">a.</span></span> <span data-ttu-id="1276a-180">選取適當的 hello**模式**。</span><span class="sxs-lookup"><span data-stu-id="1276a-180">Select hello appropriate **Mode**.</span></span>

    <span data-ttu-id="1276a-181">b.</span><span class="sxs-lookup"><span data-stu-id="1276a-181">b.</span></span> <span data-ttu-id="1276a-182">開啟 hello hello Azure 入口網站，在記事本中，從網站下載的憑證移除 hello **---BEGIN CERTIFICATE---**和**---憑證結尾---**標記，然後貼上剩餘的內容中的 hellohello**金鑰**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="1276a-182">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Key** textbox.</span></span>
    
    <span data-ttu-id="1276a-183">c.</span><span class="sxs-lookup"><span data-stu-id="1276a-183">c.</span></span> <span data-ttu-id="1276a-184">在 hello **Id 屬性**，選取 hello 適當設定的 hello hello （例如，如果是在 Azure AD 中已選取的 hello userprinciplename 則會在這裡選取的使用者名稱。） 的 Azure AD 中的使用者識別碼屬性</span><span class="sxs-lookup"><span data-stu-id="1276a-184">In hello **Id Property**, select hello appropriate attribute which you have configured as hello user identifier in hello Azure AD (For example, If hello userprinciplename is selected in Azure AD, then Username would be selected here.)</span></span>

    <span data-ttu-id="1276a-185">d.</span><span class="sxs-lookup"><span data-stu-id="1276a-185">d.</span></span> <span data-ttu-id="1276a-186">在 hello**登入 URL**，貼上 hello **「 SAML 單一登入服務 URL 」** hello 從複製的值**設定登入**hello Azure 入口網站的視窗。</span><span class="sxs-lookup"><span data-stu-id="1276a-186">In hello **Login URL**, paste hello **“SAML Single Sign-On Service URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

    <span data-ttu-id="1276a-187">e.</span><span class="sxs-lookup"><span data-stu-id="1276a-187">e.</span></span> <span data-ttu-id="1276a-188">在 hello**登出 URL**，貼上 hello **「 登出 URL 」** hello 從複製的值**設定登入**hello Azure 入口網站視窗。</span><span class="sxs-lookup"><span data-stu-id="1276a-188">In hello **Logout URL**, paste hello **“Sign-Out URL”** value you have copied from hello **Configure sign-on** window of hello Azure portal.</span></span>

13. <span data-ttu-id="1276a-189">啟用 [只允許 SSO 登入]。</span><span class="sxs-lookup"><span data-stu-id="1276a-189">Enable **‘Only Allow SSO Login’**.</span></span>

    ![設定單一登入](./media/active-directory-saas-absorblms-tutorial/5.png)

14. <span data-ttu-id="1276a-191">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1276a-191">Click **"Save."**</span></span>

> [!TIP]
> <span data-ttu-id="1276a-192">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="1276a-192">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1276a-193">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="1276a-193">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1276a-194">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1276a-194">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="1276a-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1276a-195">Create an Azure AD test user</span></span>

<span data-ttu-id="1276a-196">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1276a-196">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="1276a-198">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1276a-198">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1276a-199">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="1276a-199">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![hello Azure Active Directory 按鈕](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1276a-201">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="1276a-201">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![hello 「 使用者和群組 」 和 「 所有使用者 」 連結](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1276a-203">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1276a-203">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![hello [新增] 按鈕](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1276a-205">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-205">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![hello [使用者] 對話方塊](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1276a-207">a.</span><span class="sxs-lookup"><span data-stu-id="1276a-207">a.</span></span> <span data-ttu-id="1276a-208">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1276a-208">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1276a-209">b.</span><span class="sxs-lookup"><span data-stu-id="1276a-209">b.</span></span> <span data-ttu-id="1276a-210">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="1276a-210">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1276a-211">c.</span><span class="sxs-lookup"><span data-stu-id="1276a-211">c.</span></span> <span data-ttu-id="1276a-212">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="1276a-212">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1276a-213">d.</span><span class="sxs-lookup"><span data-stu-id="1276a-213">d.</span></span> <span data-ttu-id="1276a-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1276a-214">Click **Create**.</span></span>

### <a name="create-an-absorb-lms-test-user"></a><span data-ttu-id="1276a-215">建立 Absorb LMS 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1276a-215">Create an Absorb LMS test user</span></span>

<span data-ttu-id="1276a-216">tooenable Azure AD 使用者 toolog 中 tooAbsorb LMS，必須將他們佈建 tooAbsorb LMS 中。</span><span class="sxs-lookup"><span data-stu-id="1276a-216">tooenable Azure AD users toolog in tooAbsorb LMS, they must be provisioned in tooAbsorb LMS.</span></span>  
<span data-ttu-id="1276a-217">就 Absorb LMS 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="1276a-217">For Absorb LMS, provisioning is a manual task.</span></span>

<span data-ttu-id="1276a-218">**tooprovision 使用者帳戶，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1276a-218">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="1276a-219">登入 tooyour 吸收 LMS 公司網站的系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="1276a-219">Log in tooyour Absorb LMS company site as an administrator.</span></span>

2. <span data-ttu-id="1276a-220">按一下 [使用者] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1276a-220">Click **Users** tab.</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. <span data-ttu-id="1276a-222">按一下**使用者**下 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="1276a-222">Click **Users** under hello **Users** tab.</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  <span data-ttu-id="1276a-224">從 [新增] 下拉式清單選取 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="1276a-224">Select **User** from **Add New** drop-down.</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. <span data-ttu-id="1276a-226">在 hello**新增使用者**頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1276a-226">On hello **Add User** page, perform hello following steps:</span></span>

    ![邀請人員](./media/active-directory-saas-absorblms-tutorial/user.png)

    <span data-ttu-id="1276a-228">a.</span><span class="sxs-lookup"><span data-stu-id="1276a-228">a.</span></span> <span data-ttu-id="1276a-229">在 hello**名字**文字方塊中，類型許像 hello 名字。</span><span class="sxs-lookup"><span data-stu-id="1276a-229">In hello **First Name** textbox, type hello first name like Britta.</span></span>

    <span data-ttu-id="1276a-230">b.</span><span class="sxs-lookup"><span data-stu-id="1276a-230">b.</span></span> <span data-ttu-id="1276a-231">在 hello**姓氏**文字方塊中，型別 hello 最後一個名稱，Simon 例如。</span><span class="sxs-lookup"><span data-stu-id="1276a-231">In hello **Last Name** textbox, type hello last name like Simon.</span></span>
    
    <span data-ttu-id="1276a-232">c.</span><span class="sxs-lookup"><span data-stu-id="1276a-232">c.</span></span> <span data-ttu-id="1276a-233">在 hello **Username**文字方塊中，輸入 hello 的使用者名稱，例如許 Simon。</span><span class="sxs-lookup"><span data-stu-id="1276a-233">In hello **Username** textbox, type hello user name like Britta Simon.</span></span>

    <span data-ttu-id="1276a-234">d.</span><span class="sxs-lookup"><span data-stu-id="1276a-234">d.</span></span> <span data-ttu-id="1276a-235">在 hello**密碼**文字方塊中，類型許 Simon hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="1276a-235">In hello **Password** textbox, type hello password of Britta Simon.</span></span>

    <span data-ttu-id="1276a-236">e.</span><span class="sxs-lookup"><span data-stu-id="1276a-236">e.</span></span> <span data-ttu-id="1276a-237">在 hello**確認密碼**文字方塊中，型別 hello 相同的密碼。</span><span class="sxs-lookup"><span data-stu-id="1276a-237">In hello **Confirm Password** textbox, type hello same password.</span></span>
    
    <span data-ttu-id="1276a-238">f.</span><span class="sxs-lookup"><span data-stu-id="1276a-238">f.</span></span> <span data-ttu-id="1276a-239">使其 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="1276a-239">Make it as **ACTIVE**.</span></span>   

6. <span data-ttu-id="1276a-240">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="1276a-240">Click **"Save."**</span></span>
 
### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="1276a-241">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1276a-241">Assign hello Azure AD test user</span></span>

<span data-ttu-id="1276a-242">在本節中，您可以授與存取 tooAbsorb LMS 啟用許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1276a-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAbsorb LMS.</span></span>

![指派 hello 使用者角色][200]

<span data-ttu-id="1276a-244">**tooassign 許 Simon tooAbsorb LMS，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="1276a-244">**tooassign Britta Simon tooAbsorb LMS, perform hello following steps:**</span></span>

1. <span data-ttu-id="1276a-245">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="1276a-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1276a-247">在 [hello] 應用程式清單中，選取**吸收 LMS**。</span><span class="sxs-lookup"><span data-stu-id="1276a-247">In hello applications list, select **Absorb LMS**.</span></span>

    ![hello 應用程式清單中的 hello 吸收 LMS 連結](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. <span data-ttu-id="1276a-249">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="1276a-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![hello 「 使用者和群組 」 的連結][202] 

4. <span data-ttu-id="1276a-251">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1276a-251">Click **Add** button.</span></span> <span data-ttu-id="1276a-252">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1276a-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![hello 將作業加入窗格][203]

5. <span data-ttu-id="1276a-254">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="1276a-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1276a-255">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1276a-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1276a-256">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1276a-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="1276a-257">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1276a-257">Test single sign-on</span></span>

<span data-ttu-id="1276a-258">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="1276a-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1276a-259">按一下的 hello 吸收 LMS 磚 hello 存取面板中就會自動登入 tooyour 吸收 LMS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1276a-259">Click hello Absorb LMS tile in hello Access Panel, you will get automatically signed-on tooyour Absorb LMS application.</span></span> <span data-ttu-id="1276a-260">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](https://msdn.microsoft.com/library/dn308586)。</span><span class="sxs-lookup"><span data-stu-id="1276a-260">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1276a-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="1276a-261">Additional resources</span></span>

* [<span data-ttu-id="1276a-262">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1276a-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1276a-263">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1276a-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

