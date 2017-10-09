---
title: "教學課程：Azure Active Directory 與 Zscaler Private Access (ZPA) 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 Zscaler 私用存取 (ZPA) 之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="66106-103">教學課程：Azure Active Directory 與 Zscaler Private Access (ZPA) 整合</span><span class="sxs-lookup"><span data-stu-id="66106-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="66106-104">在此教學課程中，您學會如何 toointegrate Zscaler 私用存取 (ZPA)，與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="66106-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="66106-105">整合 Azure AD 與 Zscaler 私用存取 (ZPA) 可以提供下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="66106-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="66106-106">您可以控制存取 tooZscaler 私用存取 (ZPA) 的 Azure AD 中</span><span class="sxs-lookup"><span data-stu-id="66106-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="66106-107">您可以使用其 Azure AD 帳戶啟用您的使用者 tooautomatically get 登入 tooZscaler 私用存取 (ZPA) （單一登入）</span><span class="sxs-lookup"><span data-stu-id="66106-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="66106-108">您可以管理您的帳戶，在單一中央位置-hello Azure 管理入口網站</span><span class="sxs-lookup"><span data-stu-id="66106-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="66106-109">如果您想 tooknow 詳細與 Azure AD SaaS 應用程式整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="66106-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66106-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="66106-110">Prerequisites</span></span>

<span data-ttu-id="66106-111">tooconfigure Azure AD 整合與 Zscaler 私用存取 (ZPA)，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="66106-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="66106-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66106-112">An Azure AD subscription</span></span>
- <span data-ttu-id="66106-113">啟用 Zscaler Private Access (ZPA) 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="66106-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="66106-114">本教學課程中的步驟 tootest hello，不建議使用實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="66106-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="66106-115">在本教學課程 tootest hello 步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="66106-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="66106-116">除非必要，否則您不應使用生產環境，。</span><span class="sxs-lookup"><span data-stu-id="66106-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="66106-117">如果您沒有 Azure AD 試用環境，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="66106-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="66106-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="66106-118">Scenario description</span></span>
<span data-ttu-id="66106-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66106-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="66106-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="66106-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="66106-121">從 hello 圖庫加入 Zscaler 私用存取 (ZPA)</span><span class="sxs-lookup"><span data-stu-id="66106-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="66106-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66106-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="66106-123">從 hello 圖庫加入 Zscaler 私用存取 (ZPA)</span><span class="sxs-lookup"><span data-stu-id="66106-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="66106-124">tooconfigure hello 整合的 Zscaler 私用存取 (ZPA) 至 Azure AD，您需要從受管理的 SaaS 應用程式的 hello 圖庫 tooyour 清單 tooadd Zscaler 私用存取 (ZPA)。</span><span class="sxs-lookup"><span data-stu-id="66106-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="66106-125">**tooadd Zscaler 私用存取 (ZPA)，從 hello 組件庫中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66106-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="66106-126">在 hello  **[Azure 管理入口網站](https://portal.azure.com)**，請在 hello 左邊的導覽面板中按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="66106-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="66106-128">瀏覽過**企業應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66106-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="66106-129">然後跳過**所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66106-129">Then go too**All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="66106-131">按一下**新增**上 hello hello 對話方塊上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="66106-133">在 [hello] 搜尋方塊中，輸入**Zscaler 私用存取 (ZPA)**。</span><span class="sxs-lookup"><span data-stu-id="66106-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="66106-135">在 hello 結果 窗格中，選取  **Zscaler 私用存取 (ZPA)**，然後按一下**新增**按鈕 tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66106-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="66106-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66106-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="66106-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Zscaler Private Access (ZPA) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66106-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="66106-139">單一登入 toowork，Azure AD 需要 tooknow hello 的對等項目的使用者中 Zscaler 私用存取 (ZPA) 是 tooa 使用者在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="66106-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="66106-140">換句話說，Azure AD 使用者與 hello 相關的使用者在 Zscaler 私用存取 (ZPA) 之間的連結關聯性需要 toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="66106-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="66106-141">此連結關聯性建立 hello 將值指派為 hello**使用者名稱**做為 hello hello 值的 Azure AD 中**Username**中 Zscaler 私用存取 (ZPA)。</span><span class="sxs-lookup"><span data-stu-id="66106-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="66106-142">tooconfigure 和測試 Azure AD 單一登入與 Zscaler 私用存取 (ZPA)，您需要遵循的建置組塊 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="66106-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="66106-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** -tooenable 使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="66106-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="66106-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** -tootest Azure AD 單一登入與許 Simon。</span><span class="sxs-lookup"><span data-stu-id="66106-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="66106-145">**[建立 Zscaler 私用存取 (ZPA) 測試使用者](#creating-a-zscaler-private-access-(zpa)-test-user)** -toohave 許 Simon 中 Zscaler 私用存取 (ZPA) 是連結的 toohello Azure AD 的她的表示法的對應項目。</span><span class="sxs-lookup"><span data-stu-id="66106-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="66106-146">**[指派 hello Azure AD 的測試使用者](#assigning-the-azure-ad-test-user)** -tooenable 許 Simon toouse Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66106-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="66106-147">**[測試單一登入](#testing-single-sign-on)** -tooverify 是否 hello 組態工作。</span><span class="sxs-lookup"><span data-stu-id="66106-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="66106-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="66106-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="66106-149">在本節中，您可以啟用 Azure AD 單一登入 hello Azure 管理入口網站中，並設定單一登入 Zscaler 私用存取 (ZPA) 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="66106-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="66106-150">**Azure AD 單一登入的 tooconfigure 與 Zscaler 私用存取 (ZPA)，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66106-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="66106-151">在 hello Azure 管理入口網站上 hello **Zscaler 私用存取 (ZPA)**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="66106-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="66106-153">在 [hello**單一登入**] 對話方塊中，做為**模式**選取**SAML 型登入**tooenable 單一登入。</span><span class="sxs-lookup"><span data-stu-id="66106-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="66106-155">在 hello **Zscaler 私用存取 (ZPA) 網域和 Url**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66106-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="66106-157">a.</span><span class="sxs-lookup"><span data-stu-id="66106-157">a.</span></span> <span data-ttu-id="66106-158">在 hello**登入 URL**文字方塊中，輸入 URL，使用下列模式的 hello:`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="66106-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="66106-159">b.</span><span class="sxs-lookup"><span data-stu-id="66106-159">b.</span></span> <span data-ttu-id="66106-160">在 hello**識別碼**文字方塊中，輸入：`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="66106-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="66106-161">請注意這些不是 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="66106-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="66106-162">您有的 tooupdate 這些值與實際的 hello 登入 URL 和識別碼。</span><span class="sxs-lookup"><span data-stu-id="66106-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="66106-163">這裡我們建議您 toouse hello 中唯一值的 URL hello 識別項。</span><span class="sxs-lookup"><span data-stu-id="66106-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="66106-164">請連絡[Zscaler 私用存取 (ZPA) 支援小組](https://help.zscaler.com/zpa-submit-ticket)tooget 這些值。</span><span class="sxs-lookup"><span data-stu-id="66106-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="66106-165">在 hello **SAML 簽章憑證**區段中，按一下**建立新憑證**。</span><span class="sxs-lookup"><span data-stu-id="66106-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="66106-167">在 [hello**建立新的憑證**] 對話方塊中，按一下 hello 日曆圖示，然後選取**到期日**。</span><span class="sxs-lookup"><span data-stu-id="66106-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="66106-168">然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-168">Then click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="66106-170">在 hello **SAML 簽章憑證**區段中，選取**啟用新的憑證**按一下**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="66106-172">Hello 快顯視窗上**變換憑證**視窗中，按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="66106-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="66106-174">在 hello **SAML 簽章憑證**區段中，按一下**中繼資料 XML**然後儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="66106-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="66106-176">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zscaler Private Access (ZPA) 公司網站。</span><span class="sxs-lookup"><span data-stu-id="66106-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="66106-177">瀏覽過**管理員**，然後按一下 **Idp 組態**。</span><span class="sxs-lookup"><span data-stu-id="66106-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="66106-179">在 hello **Idp 組態**區段中，按一下**加入新的 IDP 組態**。</span><span class="sxs-lookup"><span data-stu-id="66106-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="66106-181">在 hello**新 IDP 組態**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66106-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="66106-183">a.</span><span class="sxs-lookup"><span data-stu-id="66106-183">a.</span></span> <span data-ttu-id="66106-184">按一下 [選取檔案]，然後上傳您下載的中繼資料檔。</span><span class="sxs-lookup"><span data-stu-id="66106-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="66106-185">b.</span><span class="sxs-lookup"><span data-stu-id="66106-185">b.</span></span> <span data-ttu-id="66106-186">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="66106-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66106-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="66106-188">hello 本節目標在於 toocreate 呼叫許 Simon hello Azure 管理入口網站中的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="66106-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="66106-190">**toocreate 測試使用者在 Azure AD 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66106-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="66106-191">在 hello **Azure 管理入口網站**，在 hello 左側的導覽窗格中，按一下**Azure Active Directory**圖示。</span><span class="sxs-lookup"><span data-stu-id="66106-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="66106-193">跳過**使用者和群組**按一下**所有使用者**toodisplay hello 使用者清單。</span><span class="sxs-lookup"><span data-stu-id="66106-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="66106-195">在 hello hello 對話方塊頂端按一下**新增**tooopen hello**使用者**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="66106-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="66106-197">在 hello**使用者**對話方塊頁面上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="66106-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="66106-199">a.</span><span class="sxs-lookup"><span data-stu-id="66106-199">a.</span></span> <span data-ttu-id="66106-200">在 hello**名稱**文字方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="66106-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="66106-201">b.</span><span class="sxs-lookup"><span data-stu-id="66106-201">b.</span></span> <span data-ttu-id="66106-202">在 hello**使用者名**文字方塊中，型別 hello**電子郵件地址**BrittaSimon。</span><span class="sxs-lookup"><span data-stu-id="66106-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="66106-203">c.</span><span class="sxs-lookup"><span data-stu-id="66106-203">c.</span></span> <span data-ttu-id="66106-204">選取**顯示密碼**記下 hello hello 值**密碼**。</span><span class="sxs-lookup"><span data-stu-id="66106-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="66106-205">d.</span><span class="sxs-lookup"><span data-stu-id="66106-205">d.</span></span> <span data-ttu-id="66106-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="66106-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="66106-207">建立 Zscaler Private Access (ZPA) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="66106-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="66106-208">在本節中，您要在 Zscaler Private Access (ZPA) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="66106-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="66106-209">請使用[Zscaler 私用存取 (ZPA) 支援小組](https://help.zscaler.com/zpa-submit-ticket)tooadd hello hello Zscaler 私用存取 (ZPA) 平台的使用者。</span><span class="sxs-lookup"><span data-stu-id="66106-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="66106-210">指派 hello Azure AD 的測試使用者</span><span class="sxs-lookup"><span data-stu-id="66106-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="66106-211">在本節中，以啟用許 Simon toouse Azure 單一登入授與他們存取 tooZscaler 私用存取 (ZPA)。</span><span class="sxs-lookup"><span data-stu-id="66106-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![指派使用者][200] 

<span data-ttu-id="66106-213">**tooassign 許 Simon tooZscaler 私用存取 (ZPA) 執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="66106-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="66106-214">在 hello Azure 管理入口網站中，開啟 hello 應用程式 檢視，然後導覽 toohello 目錄檢視，並跳過**企業應用程式**然後按一下 **所有應用程式**。</span><span class="sxs-lookup"><span data-stu-id="66106-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="66106-216">在 [hello] 應用程式清單中，選取**Zscaler 私用存取 (ZPA)**。</span><span class="sxs-lookup"><span data-stu-id="66106-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![設定單一登入](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="66106-218">在左側 hello hello 功能表上，按一下**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="66106-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="66106-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-220">Click **Add** button.</span></span> <span data-ttu-id="66106-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="66106-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="66106-223">在**使用者和群組**對話方塊中，選取**許 Simon** hello 使用者 清單中。</span><span class="sxs-lookup"><span data-stu-id="66106-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="66106-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="66106-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="66106-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="66106-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="66106-226">Testing single sign-on</span></span>

<span data-ttu-id="66106-227">在本節中，您可以測試您 Azure AD 單一登入的組態 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="66106-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="66106-228">當您按一下 hello Zscaler 私用存取 (ZPA) 磚 hello 存取面板中的時，您應該取得 tooyour 自動登入 Zscaler 私用存取 (ZPA) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="66106-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="66106-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="66106-229">Additional resources</span></span>

* [<span data-ttu-id="66106-230">如何教學課程清單 tooIntegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66106-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="66106-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="66106-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png