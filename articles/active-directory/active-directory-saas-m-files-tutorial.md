---
title: "教學課程：Azure Active Directory 與 M-Files 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 M 檔案之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4536fd49-3a65-4cff-9620-860904f726d0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: e1d268da53312b1d2c12e29d66b1a5b66d0cdcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-m-files"></a><span data-ttu-id="eec40-103">教學課程：Azure Active Directory 與 M-Files 整合</span><span class="sxs-lookup"><span data-stu-id="eec40-103">Tutorial: Azure Active Directory integration with M-Files</span></span>

<span data-ttu-id="eec40-104">在此教學課程中，您學會如何 toointegrate M 檔案與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="eec40-104">In this tutorial, you learn how toointegrate M-Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eec40-105">與 Azure AD 整合 M 檔案可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="eec40-105">Integrating M-Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eec40-106">您可以控制存取 tooM 檔案的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="eec40-106">You can control in Azure AD who has access tooM-Files</span></span>
- <span data-ttu-id="eec40-107">您可以啟用您使用者 tooautomatically 取得已登入的 tooM-檔案 （單一登入） 具有其 Azure AD 帳戶</span><span class="sxs-lookup"><span data-stu-id="eec40-107">You can enable your users tooautomatically get signed-on tooM-Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eec40-108">您可以管理您的帳戶，在單一中央位置-hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="eec40-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eec40-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="eec40-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eec40-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="eec40-110">Prerequisites</span></span>

<span data-ttu-id="eec40-111">tooconfigure 與 M 檔案的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="eec40-111">tooconfigure Azure AD integration with M-Files, you need hello following items:</span></span>

- <span data-ttu-id="eec40-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="eec40-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eec40-113">已啟用 M-Files 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="eec40-113">A M-Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eec40-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="eec40-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eec40-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="eec40-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eec40-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="eec40-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eec40-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="eec40-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eec40-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="eec40-118">Scenario description</span></span>
<span data-ttu-id="eec40-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="eec40-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eec40-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="eec40-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eec40-121">從 hello 圖庫加入 M 檔案</span><span class="sxs-lookup"><span data-stu-id="eec40-121">Adding M-Files from hello gallery</span></span>
2. <span data-ttu-id="eec40-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="eec40-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-m-files-from-hello-gallery"></a><span data-ttu-id="eec40-123">從 hello 圖庫加入 M 檔案</span><span class="sxs-lookup"><span data-stu-id="eec40-123">Adding M-Files from hello gallery</span></span>
<span data-ttu-id="eec40-124">tooconfigure hello 整合 M 檔案到 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd M 檔案。</span><span class="sxs-lookup"><span data-stu-id="eec40-124">tooconfigure hello integration of M-Files into Azure AD, you need tooadd M-Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eec40-125">**tooadd M 檔案從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="eec40-125">**tooadd M-Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eec40-126">在 hello  **[Azure 入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="eec40-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eec40-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="eec40-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eec40-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="eec40-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="eec40-131">tooadd 新應用程式中，按一下 **新的應用程式**上 hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="eec40-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="eec40-133">在 [hello] 搜尋方塊中，輸入**M 檔案**。</span><span class="sxs-lookup"><span data-stu-id="eec40-133">In hello search box, type **M-Files**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_search.png)

5. <span data-ttu-id="eec40-135">在 hello 結果 窗格中，選取  **M 檔案**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eec40-135">In hello results panel, select **M-Files**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eec40-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="eec40-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eec40-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 M-Files 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="eec40-138">In this section, you configure and test Azure AD single sign-on with M-Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eec40-139">單一登入 toowork，Azure AD 需要 tooknow M 檔案中的 hello 對等項目的使用者是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="eec40-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in M-Files is tooa user in Azure AD.</span></span> <span data-ttu-id="eec40-140">換句話說，Azure AD 使用者與 M 檔案中的 hello 相關的使用者之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="eec40-140">In other words, a link relationship between an Azure AD user and hello related user in M-Files needs toobe established.</span></span>

<span data-ttu-id="eec40-141">M 檔案中指派的 hello hello 值**使用者名稱**做為 hello hello 值的 Azure AD 中**Username** tooestablish hello 連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="eec40-141">In M-Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eec40-142">tooconfigure 及測試 Azure AD 單一登入與 M 檔案，您必須遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="eec40-142">tooconfigure and test Azure AD single sign-on with M-Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eec40-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="eec40-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eec40-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="eec40-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eec40-145">**[建立測試使用者 M 檔案](#creating-a-m-files-test-user)** -toohave 是連結的 toohello Azure AD 使用者表示法的許 Simon M 檔案中對應項目。</span><span class="sxs-lookup"><span data-stu-id="eec40-145">**[Creating a M-Files test user](#creating-a-m-files-test-user)** - toohave a counterpart of Britta Simon in M-Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eec40-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="eec40-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eec40-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="eec40-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eec40-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="eec40-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eec40-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 入口網站中，並 M 檔案應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="eec40-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your M-Files application.</span></span>

<span data-ttu-id="eec40-150">**tooconfigure Azure AD 單一登入 M 檔案時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="eec40-150">**tooconfigure Azure AD single sign-on with M-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="eec40-151">在 Azure 入口網站上 hello hello **M 檔案**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="eec40-151">In hello Azure portal, on hello **M-Files** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="eec40-153">在 hello**單一登入**對話方塊中，選取**模式**為**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="eec40-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_samlbase.png)

3. <span data-ttu-id="eec40-155">在 hello **M 檔案網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="eec40-155">On hello **M-Files Domain and URLs** section, perform hello following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_url.png)

    <span data-ttu-id="eec40-157">a.</span><span class="sxs-lookup"><span data-stu-id="eec40-157">a.</span></span> <span data-ttu-id="eec40-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span><span class="sxs-lookup"><span data-stu-id="eec40-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com/authentication/MFiles.AuthenticationProviders.Core/sso`</span></span>

    <span data-ttu-id="eec40-159">b.</span><span class="sxs-lookup"><span data-stu-id="eec40-159">b.</span></span> <span data-ttu-id="eec40-160">在 hello**識別碼**文字方塊中，輸入 URL，使用下列模式的 hello:`https://<tenantname>.cloudvault.m-files.com`</span><span class="sxs-lookup"><span data-stu-id="eec40-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.cloudvault.m-files.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eec40-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="eec40-161">These values are not real.</span></span> <span data-ttu-id="eec40-162">更新這些值與實際的 hello 登入 URL 和識別項。</span><span class="sxs-lookup"><span data-stu-id="eec40-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eec40-163">請連絡[M 檔案用戶端支援小組](mailto:support@m-files.com)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="eec40-163">Contact [M-Files Client support team](mailto:support@m-files.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="eec40-164">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="eec40-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_certificate.png) 

5. <span data-ttu-id="eec40-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="eec40-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eec40-168">tooget SSO 設定應用程式，請連絡[M 檔案支援小組](mailto:support@m-files.com)並提供給他們 hello 下載中繼資料。</span><span class="sxs-lookup"><span data-stu-id="eec40-168">tooget SSO configured for your application, contact [M-Files support team](mailto:support@m-files.com) and provide them hello downloaded Metadata.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="eec40-169">如果您想要您 M 檔案桌面應用程式 tooconfigure SSO，請遵循 hello 接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="eec40-169">Follow hello next steps if you want tooconfigure SSO for you M-File desktop application.</span></span> <span data-ttu-id="eec40-170">如果您只想 tooconfigure SSO M 檔案 web 版本，不不需要任何額外的步驟。</span><span class="sxs-lookup"><span data-stu-id="eec40-170">No extra steps are required if you only want tooconfigure SSO for M-Files web version.</span></span>  

7. <span data-ttu-id="eec40-171">請遵循 hello 下一個步驟 tooconfigure hello M 檔案桌面應用程式 tooenable 與 Azure AD 的 SSO。</span><span class="sxs-lookup"><span data-stu-id="eec40-171">Follow hello next steps tooconfigure hello M-File desktop application tooenable SSO with Azure AD.</span></span> <span data-ttu-id="eec40-172">toodownload M 檔案太移[M 檔案下載](https://www.m-files.com/en/download-latest-version)頁面。</span><span class="sxs-lookup"><span data-stu-id="eec40-172">toodownload M-Files, go too[M-Files download](https://www.m-files.com/en/download-latest-version) page.</span></span>

8. <span data-ttu-id="eec40-173">開啟 hello **M 檔案桌面設定**視窗。</span><span class="sxs-lookup"><span data-stu-id="eec40-173">Open hello **M-Files Desktop Settings** window.</span></span> <span data-ttu-id="eec40-174">然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="eec40-174">Then, click **Add**.</span></span>
   
    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_10.png)

9. <span data-ttu-id="eec40-176">在 hello**文件保存庫的連接屬性**視窗中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="eec40-176">On hello **Document Vault Connection Properties** window, perform hello following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m_files_11.png)  

    <span data-ttu-id="eec40-178">Hello 伺服器區段類型，在 hello，如下所示的值：</span><span class="sxs-lookup"><span data-stu-id="eec40-178">Under hello Server section type, hello values as follows:</span></span>  

    <span data-ttu-id="eec40-179">a.</span><span class="sxs-lookup"><span data-stu-id="eec40-179">a.</span></span> <span data-ttu-id="eec40-180">在 [名稱] 中，輸入 `<tenant-name>.cloudvault.m-files.com`。</span><span class="sxs-lookup"><span data-stu-id="eec40-180">For **Name**, type `<tenant-name>.cloudvault.m-files.com`.</span></span> 
 
    <span data-ttu-id="eec40-181">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="eec40-181">b.</span></span> <span data-ttu-id="eec40-182">在 [連接埠號碼]中，輸入 **4466**。</span><span class="sxs-lookup"><span data-stu-id="eec40-182">For **Port Number**, type **4466**.</span></span> 

    <span data-ttu-id="eec40-183">c.</span><span class="sxs-lookup"><span data-stu-id="eec40-183">c.</span></span> <span data-ttu-id="eec40-184">在 [通訊協定]中，選取 **HTTPS**。</span><span class="sxs-lookup"><span data-stu-id="eec40-184">For **Protocol**, select **HTTPS**.</span></span> 

    <span data-ttu-id="eec40-185">d.</span><span class="sxs-lookup"><span data-stu-id="eec40-185">d.</span></span> <span data-ttu-id="eec40-186">在 hello**驗證**欄位中，選取**特定的 Windows 使用者**。</span><span class="sxs-lookup"><span data-stu-id="eec40-186">In hello **Authentication** field, select **Specific Windows user**.</span></span> <span data-ttu-id="eec40-187">然後，系統會向您提示簽署頁面。</span><span class="sxs-lookup"><span data-stu-id="eec40-187">Then, you are prompted with a signing page.</span></span> <span data-ttu-id="eec40-188">請插入您的 Azure AD 認證。</span><span class="sxs-lookup"><span data-stu-id="eec40-188">Insert your Azure AD credentials.</span></span> 

    <span data-ttu-id="eec40-189">e.</span><span class="sxs-lookup"><span data-stu-id="eec40-189">e.</span></span> <span data-ttu-id="eec40-190">Hello**伺服器上的保存庫**，選取 hello 伺服器上對應的保存庫。</span><span class="sxs-lookup"><span data-stu-id="eec40-190">For hello **Vault on Server**,  select hello corresponding vault on server.</span></span>
 
    <span data-ttu-id="eec40-191">f.</span><span class="sxs-lookup"><span data-stu-id="eec40-191">f.</span></span> <span data-ttu-id="eec40-192">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="eec40-192">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="eec40-193">您現在可以讀取這些指示在 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定 hello 應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="eec40-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eec40-194">加入此應用程式從 hello 之後**Active Directory > 企業應用程式**區段中，只要按一下 hello**單一登入** 索引標籤和存取 hello 內嵌文件，透過 hello **組態**hello 底部的區段。</span><span class="sxs-lookup"><span data-stu-id="eec40-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eec40-195">閱讀更多有關 hello embedded 文件功能： [Azure AD 的內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eec40-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eec40-196">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="eec40-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="eec40-197">hello 本節目標在於 toocreate hello 呼叫許 Simon 的 Azure 入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="eec40-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="eec40-199">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="eec40-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eec40-200">在 hello **Azure 入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="eec40-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eec40-202">toodisplay hello 使用者清單，請移過**使用者和群組**按一下**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="eec40-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eec40-204">tooopen hello**使用者**] 對話方塊中，按一下 [**新增**上 hello hello 對話方塊的頂端。</span><span class="sxs-lookup"><span data-stu-id="eec40-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eec40-206">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="eec40-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-m-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eec40-208">a.</span><span class="sxs-lookup"><span data-stu-id="eec40-208">a.</span></span> <span data-ttu-id="eec40-209">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="eec40-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eec40-210">b.</span><span class="sxs-lookup"><span data-stu-id="eec40-210">b.</span></span> <span data-ttu-id="eec40-211">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="eec40-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eec40-212">c.</span><span class="sxs-lookup"><span data-stu-id="eec40-212">c.</span></span> <span data-ttu-id="eec40-213">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="eec40-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eec40-214">d.</span><span class="sxs-lookup"><span data-stu-id="eec40-214">d.</span></span> <span data-ttu-id="eec40-215">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="eec40-215">Click **Create**.</span></span>
 
### <a name="creating-a-m-files-test-user"></a><span data-ttu-id="eec40-216">建立 M-Files 測試使用者</span><span class="sxs-lookup"><span data-stu-id="eec40-216">Creating a M-Files test user</span></span>

<span data-ttu-id="eec40-217">hello 本節目標在於 toocreate 呼叫許 Simon M 檔案中的使用者。</span><span class="sxs-lookup"><span data-stu-id="eec40-217">hello objective of this section is toocreate a user called Britta Simon in M-Files.</span></span> <span data-ttu-id="eec40-218">使用[M 檔案支援小組](mailto:support@m-files.com)tooadd hello 使用者 hello M 檔案中的。</span><span class="sxs-lookup"><span data-stu-id="eec40-218">Work with  [M-Files support team](mailto:support@m-files.com) tooadd hello users in hello M-Files.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eec40-219">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="eec40-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eec40-220">本節中，您可以授與存取 tooM 檔案啟用了許 Simon toouse Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="eec40-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooM-Files.</span></span>

![指派使用者][200] 

<span data-ttu-id="eec40-222">**tooassign 許 Simon tooM 檔案，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="eec40-222">**tooassign Britta Simon tooM-Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="eec40-223">在 hello Azure 入口網站，開啟 hello 應用程式檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="eec40-223">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="eec40-225">在 [hello] 應用程式清單中，選取**M 檔案**。</span><span class="sxs-lookup"><span data-stu-id="eec40-225">In hello applications list, select **M-Files**.</span></span>

    ![設定單一登入](./media/active-directory-saas-m-files-tutorial/tutorial_m-files_app.png) 

3. <span data-ttu-id="eec40-227">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="eec40-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="eec40-229">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eec40-229">Click **Add** button.</span></span> <span data-ttu-id="eec40-230">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="eec40-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="eec40-232">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="eec40-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eec40-233">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eec40-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eec40-234">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="eec40-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eec40-235">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="eec40-235">Testing single sign-on</span></span>

<span data-ttu-id="eec40-236">hello 本節目標在於 tootest 您 Azure AD 的 SSO 組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="eec40-236">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="eec40-237">當您按一下 hello M 檔案磚 hello 存取面板中，您應該取得自動登入 tooyour M 檔案的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eec40-237">When you click hello M-Files tile in hello Access Panel, you should get automatically signed-on tooyour M-Files application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eec40-238">其他資源</span><span class="sxs-lookup"><span data-stu-id="eec40-238">Additional resources</span></span>

* [<span data-ttu-id="eec40-239">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eec40-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eec40-240">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="eec40-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-m-files-tutorial/tutorial_general_203.png

