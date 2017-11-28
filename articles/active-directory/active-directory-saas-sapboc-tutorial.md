---
title: "教學課程：Azure Active Directory 與 SAP Business Object Cloud 整合 | Microsoft Docs"
description: "了解 tooconfigure 的單一登入 Azure Active Directory 與 SAP 商務物件雲端之間。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 6c5e44f0-4e52-463f-b879-834d80a55cdf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: a3e9bd93897271531f91bcbc50cd361e8a20551e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-object-cloud"></a><span data-ttu-id="e2b53-103">教學課程：Azure Active Directory 與 SAP Business Object Cloud 整合</span><span class="sxs-lookup"><span data-stu-id="e2b53-103">Tutorial: Azure Active Directory integration with SAP Business Object Cloud</span></span>

<span data-ttu-id="e2b53-104">在此教學課程中，您學習如何 toointegrate SAP 商務物件雲端與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-104">In this tutorial, you learn how toointegrate SAP Business Object Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2b53-105">您會收到 hello 與 Azure AD 整合 SAP 商務物件雲端時，下列優點：</span><span class="sxs-lookup"><span data-stu-id="e2b53-105">You get hello following benefits when you integrate SAP Business Object Cloud with Azure AD:</span></span>

- <span data-ttu-id="e2b53-106">在 Azure AD 中，您可以控制誰可以存取 tooSAP 商務物件的雲端。</span><span class="sxs-lookup"><span data-stu-id="e2b53-106">In Azure AD, you can control who has access tooSAP Business Object Cloud.</span></span>
- <span data-ttu-id="e2b53-107">您可以自動登入您的使用者 tooSAP 商務物件雲端使用單一登入和使用者的 Azure AD 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2b53-107">You can automatically sign in your users tooSAP Business Object Cloud by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="e2b53-108">您可以管理您的帳戶，在一個集中位置，hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e2b53-108">You can manage your accounts in one, central location, hello Azure portal.</span></span>

<span data-ttu-id="e2b53-109">toolearn 進一步了解軟體即服務 (SaaS) 應用程式與 Azure AD 整合，請參閱[什麼是應用程式存取和單一登入與 Azure Active Directory？](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-109">toolearn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2b53-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="e2b53-110">Prerequisites</span></span>

<span data-ttu-id="e2b53-111">tooset 與 SAP 商務物件雲端的 Azure AD 整合，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="e2b53-111">tooset up Azure AD integration with SAP Business Object Cloud, you need hello following items:</span></span>

- <span data-ttu-id="e2b53-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e2b53-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2b53-113">已開啟單一登入的 SAP Business Object Cloud</span><span class="sxs-lookup"><span data-stu-id="e2b53-113">An SAP Business Object Cloud, with single sign-on turned on</span></span>

> [!NOTE]
> <span data-ttu-id="e2b53-114">如果您在測試 hello 步驟在本教學課程，我們建議您不要在生產環境中測試它們。</span><span class="sxs-lookup"><span data-stu-id="e2b53-114">If you test hello steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="e2b53-115">測試本教學課程中的 hello 步驟建議：</span><span class="sxs-lookup"><span data-stu-id="e2b53-115">Recommendations for testing hello steps in this tutorial:</span></span>

- <span data-ttu-id="e2b53-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="e2b53-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="e2b53-117">如果您沒有 Azure AD 試用環境，可以[取得一個月的免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2b53-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="e2b53-118">Scenario description</span></span>
<span data-ttu-id="e2b53-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e2b53-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="e2b53-120">本教學課程所述的 hello 案例包含兩個主要建置組塊：</span><span class="sxs-lookup"><span data-stu-id="e2b53-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2b53-121">加入 SAP 商務物件雲端從 hello 組件庫。</span><span class="sxs-lookup"><span data-stu-id="e2b53-121">Add SAP Business Object Cloud from hello gallery.</span></span>
2. <span data-ttu-id="e2b53-122">設定和測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e2b53-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-sap-business-object-cloud-from-hello-gallery"></a><span data-ttu-id="e2b53-123">新增 SAP 商務物件雲端從 hello 組件庫</span><span class="sxs-lookup"><span data-stu-id="e2b53-123">Add SAP Business Object Cloud from hello gallery</span></span>
<span data-ttu-id="e2b53-124">SAP 商務物件雲端的 Azure ad 的 hello 圖庫中的 hello 整合 tooset SAP 商務物件雲端 tooyour 之新增受管理的 SaaS 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2b53-124">tooset up hello integration of SAP Business Object Cloud with Azure AD, in hello gallery, add SAP Business Object Cloud tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e2b53-125">tooadd hello 圖庫 SAP 商務物件雲端：</span><span class="sxs-lookup"><span data-stu-id="e2b53-125">tooadd SAP Business Object Cloud from hello gallery:</span></span>

1. <span data-ttu-id="e2b53-126">在 [hello [Azure 入口網站](https://portal.azure.com)，在 [hello 左側的功能表中選取**Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-126">In hello [Azure portal](https://portal.azure.com), in hello left menu, select **Azure Active Directory**.</span></span> 

    ![hello Azure Active Directory] 按鈕][1]

2. <span data-ttu-id="e2b53-128">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![hello 企業應用程式] 頁面][2]
    
3. <span data-ttu-id="e2b53-130">tooadd 新的應用程式中，選取**新的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-130">tooadd a new application, select **New application**.</span></span>

    ![hello 新應用程式按鈕][3]

4. <span data-ttu-id="e2b53-132">在 [hello] 搜尋方塊中，輸入**SAP 商務物件雲端**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-132">In hello search box, enter **SAP Business Object Cloud**.</span></span>

    ![hello 搜尋方塊](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_search.png)

5. <span data-ttu-id="e2b53-134">在 [hello [結果] 窗格中，選取**SAP 商務物件雲端**，然後選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-134">In hello results panel, select **SAP Business Object Cloud**, and then select **Add**.</span></span>

    ![Hello 結果清單中的 SAP 商務物件雲端](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_addfromgallery.png)

##  <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e2b53-136">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e2b53-136">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="e2b53-137">在本節中，您將以名為 Britta Simon 的測試使用者身分，設定及測試與 SAP Business Object Cloud 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="e2b53-137">In this section, you set up and test Azure AD single sign-on with SAP Business Object Cloud based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="e2b53-138">Azure AD 單一登入 toowork，需要 tooknow hello Azure AD SAP 商務物件雲端中的對等項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="e2b53-138">For single sign-on toowork, Azure AD needs tooknow hello Azure AD counterpart user in SAP Business Object Cloud.</span></span> <span data-ttu-id="e2b53-139">必須先建立 Azure AD 使用者與 SAP 商務物件雲端中的 hello 相關的使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="e2b53-139">A link relationship between an Azure AD user and hello related user in SAP Business Object Cloud must be established.</span></span>

<span data-ttu-id="e2b53-140">tooestablish hello 連結關聯性，在 SAP 商務物件雲端中，適用於**Username**，hello hello 值指派**使用者名**在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="e2b53-140">tooestablish hello link relationship, in SAP Business Object Cloud, for **Username**, assign hello value of hello **user name** in Azure AD.</span></span>

<span data-ttu-id="e2b53-141">tooconfigure 和測試 Azure AD 單一登入與 SAP 商務物件的雲端，完成下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="e2b53-141">tooconfigure and test Azure AD single sign-on with SAP Business Object Cloud, complete hello following tasks:</span></span>

1. <span data-ttu-id="e2b53-142">[設定 Azure AD 單一登入](#set-up-azure-ad-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-142">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="e2b53-143">設定使用者 toouse 這項功能。</span><span class="sxs-lookup"><span data-stu-id="e2b53-143">Sets up a user toouse this feature.</span></span>
2. <span data-ttu-id="e2b53-144">[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-144">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="e2b53-145">測試 Azure AD 單一登入與 hello 使用者許 Simon。</span><span class="sxs-lookup"><span data-stu-id="e2b53-145">Tests Azure AD single sign-on with hello user Britta Simon.</span></span>
3. <span data-ttu-id="e2b53-146">[建立 SAP Business Object Cloud 測試使用者](#create-an-sap-business-object-cloud-test-user)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-146">[Create an SAP Business Object Cloud test user](#create-an-sap-business-object-cloud-test-user).</span></span> <span data-ttu-id="e2b53-147">在 SAP 商務物件雲端連結的 toohello hello 使用者的 Azure AD 表示法建立許 Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="e2b53-147">Creates a counterpart of Britta Simon in SAP Business Object Cloud that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="e2b53-148">[指派給 Azure AD hello 測試使用者](#assign-the-azure-ad-test-user)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-148">[Assign hello Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="e2b53-149">設定 Azure AD 單一登入許 Simon toouse。</span><span class="sxs-lookup"><span data-stu-id="e2b53-149">Sets up Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2b53-150">[測試單一登入](#test-single-sign-on)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-150">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="e2b53-151">請確認該 hello 設定可正常運作。</span><span class="sxs-lookup"><span data-stu-id="e2b53-151">Verifies that hello configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="e2b53-152">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="e2b53-152">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="e2b53-153">在本節中，您開啟 Azure AD 單一登入 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e2b53-153">In this section, you turn on Azure AD single sign-on in hello Azure portal.</span></span> <span data-ttu-id="e2b53-154">然後，您要在 SAP Business Object Cloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="e2b53-154">Then, you set up single sign-on in your SAP Business Object Cloud application.</span></span>

<span data-ttu-id="e2b53-155">Azure AD 單一登入與 SAP 商務物件雲端 tooset:</span><span class="sxs-lookup"><span data-stu-id="e2b53-155">tooset up Azure AD single sign-on with SAP Business Object Cloud:</span></span>

1. <span data-ttu-id="e2b53-156">在 Azure 入口網站上 hello hello **SAP 商務物件雲端**應用程式整合頁面上，選取**單一登入**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-156">In hello Azure portal, on hello **SAP Business Object Cloud** application integration page, select **Single sign-on**.</span></span>

    ![選取 [單一登入]][4]

2. <span data-ttu-id="e2b53-158">在 hello**單一登入**] 頁面上，針對**模式**，選取**SAML 型登入**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-158">On hello **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![選取 SAML 登入](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_samlbase.png)

3. <span data-ttu-id="e2b53-160">在下**SAP 商務物件雲端網域和 Url**完整 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e2b53-160">Under **SAP Business Object Cloud Domain and URLs**, complete hello following steps:</span></span>

    1. <span data-ttu-id="e2b53-161">在 [hello**登入 URL**方塊中，輸入 URL，其中具有 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="e2b53-161">In hello **Sign-on URL** box, enter a URL that has hello following pattern:</span></span> 
    | |
    |-|-|
    | `https://<sub-domain>.sapanalytics.cloud/` |
    | `https://<sub-domain>.sapbusinessobjects.cloud/` |

    2. <span data-ttu-id="e2b53-162">在 [hello**識別碼**方塊中，輸入 URL，其中具有 hello 下列模式：</span><span class="sxs-lookup"><span data-stu-id="e2b53-162">In hello **Identifier** box, enter a URL that has hello following pattern:</span></span>
    | |
    |-|-|
    | `<sub-domain>.sapbusinessobjects.cloud` |
    | `<sub-domain>.sapanalytics.cloud` |

    ![SAP Business Object Cloud 網域和 URL 頁面的 URL](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_url.png)
 
    > [!NOTE] 
    > <span data-ttu-id="e2b53-164">這些 Url 中的 hello 值為僅供示範之。</span><span class="sxs-lookup"><span data-stu-id="e2b53-164">hello values in these URLs are for demonstration only.</span></span> <span data-ttu-id="e2b53-165">更新 hello 值與實際的 hello 登入 URL 和識別碼的 URL。</span><span class="sxs-lookup"><span data-stu-id="e2b53-165">Update hello values with hello actual sign-on URL and identifier URL.</span></span> <span data-ttu-id="e2b53-166">tooget hello 登入 URL，請連絡 hello [SAP 商務物件雲端的用戶端支援小組](https://www.sap.com/product/analytics/cloud-analytics.support.html)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-166">tooget hello sign-on URL, contact hello [SAP Business Object Cloud Client support team](https://www.sap.com/product/analytics/cloud-analytics.support.html).</span></span> <span data-ttu-id="e2b53-167">您可以藉由從 hello 系統管理員主控台下載 hello SAP 商務物件雲端中繼資料取得 hello 識別項 URL。</span><span class="sxs-lookup"><span data-stu-id="e2b53-167">You can get hello identifier URL by downloading hello SAP Business Object Cloud metadata from hello admin console.</span></span> <span data-ttu-id="e2b53-168">稍後在 hello 教學課程的說明。</span><span class="sxs-lookup"><span data-stu-id="e2b53-168">This is explained later in hello tutorial.</span></span> 

4. <span data-ttu-id="e2b53-169">在 [SAML 簽章憑證] 下，選取 [中繼資料 XML]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-169">Under **SAML Signing Certificate**, select **Metadata XML**.</span></span> <span data-ttu-id="e2b53-170">然後，儲存您的電腦上的 hello 中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="e2b53-170">Then, save hello metadata file on your computer.</span></span>

    ![選取 [中繼資料 XML]](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_certificate.png) 

5. <span data-ttu-id="e2b53-172">選取 [ **儲存**]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-172">Select **Save**.</span></span>

    ![選取 [儲存]](./media/active-directory-saas-sapboc-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e2b53-174">在不同的網頁瀏覽器視窗中，以系統管理員身分登入 tooyour SAP 商務物件雲端公司網站。</span><span class="sxs-lookup"><span data-stu-id="e2b53-174">In a different web browser window, sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

7. <span data-ttu-id="e2b53-175">選取 [功能表] > [系統] > [管理]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-175">Select **Menu** > **System** > **Administration**.</span></span>
    
    ![依序選取 [功能表]、[系統] 和 [管理]](./media/active-directory-saas-sapboc-tutorial/config1.png)

8. <span data-ttu-id="e2b53-177">在 [hello**安全性**索引標籤，選取 hello**編輯**（畫筆） 圖示。</span><span class="sxs-lookup"><span data-stu-id="e2b53-177">On hello **Security** tab, select hello **Edit** (pen) icon.</span></span>
    
    ![Hello 安全性索引標籤上，選取 [hello [編輯] 圖示](./media/active-directory-saas-sapboc-tutorial/config2.png)  

9. <span data-ttu-id="e2b53-179">選取 [SAML 單一登入 (SSO)] 作為 [驗證方法]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-179">For **Authentication Method**, select **SAML Single Sign-On (SSO)**.</span></span>

    ![選取 [SAML 單一登入 hello 驗證方法](./media/active-directory-saas-sapboc-tutorial/config3.png)  

10. <span data-ttu-id="e2b53-181">toodownload hello 服務提供者中繼資料 (步驟 1) 選取**下載**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-181">toodownload hello service provider metadata (Step 1), select **Download**.</span></span> <span data-ttu-id="e2b53-182">在 [hello 中繼資料檔，尋找並複製 hello **entityID**值。</span><span class="sxs-lookup"><span data-stu-id="e2b53-182">In hello metadata file, find and copy hello **entityID** value.</span></span> <span data-ttu-id="e2b53-183">在 hello Azure 入口網站中，在**SAP 商務物件雲端網域和 Url**，hello 值貼在 hello**識別碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="e2b53-183">In hello Azure portal, under **SAP Business Object Cloud Domain and URLs**, paste hello value in hello **Identifier** box.</span></span>

    ![複製並貼上 hello entityID 值](./media/active-directory-saas-sapboc-tutorial/config4.png)  

11. <span data-ttu-id="e2b53-185">tooupload hello 服務提供者中繼資料 (步驟 2) 在您從網站下載的 hello 檔案 hello Azure 入口網站底下**上傳的身分識別提供者中繼資料**，選取**上傳**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-185">tooupload hello service provider metadata (Step 2) in hello file that you downloaded from hello Azure portal, under **Upload Identity Provider metadata**, select **Upload**.</span></span>  

    ![在上傳識別提供者中繼資料下，選取 [上傳]](./media/active-directory-saas-sapboc-tutorial/config5.png)

12. <span data-ttu-id="e2b53-187">在 [hello**使用者屬性**清單，您在實作想 toouse 選取 hello 使用者屬性 (步驟 3)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-187">In hello **User Attribute** list, select hello user attribute (Step 3) that you want toouse for your implementation.</span></span> <span data-ttu-id="e2b53-188">此使用者屬性對應 toohello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="e2b53-188">This user attribute maps toohello identity provider.</span></span> <span data-ttu-id="e2b53-189">tooenter hello 使用者] 頁面上，使用 hello 的自訂屬性**自訂 SAML 對應**選項。</span><span class="sxs-lookup"><span data-stu-id="e2b53-189">tooenter a custom attribute on hello user's page, use hello **Custom SAML Mapping** option.</span></span> <span data-ttu-id="e2b53-190">或者，您可以選取**電子郵件**或**使用者識別碼**做 hello 使用者屬性。</span><span class="sxs-lookup"><span data-stu-id="e2b53-190">Or, you can select either **Email** or **USER ID** as hello user attribute.</span></span> <span data-ttu-id="e2b53-191">在本例中，我們選取 [**電子郵件**因為我們對應 hello 使用者識別項宣告以 hello **userprincipalname**中 hello 屬性**使用者屬性**hello > 一節Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="e2b53-191">In our example, we selected **Email** because we mapped hello user identifier claim with hello **userprincipalname** attribute in hello **User Attributes** section in hello Azure portal.</span></span> <span data-ttu-id="e2b53-192">這會提供唯一的使用者電子郵件，每個成功的 SAML 回應中傳送 toohello SAP 商務物件雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2b53-192">This provides a unique user email, which is sent toohello SAP Business Object Cloud application in every successful SAML response.</span></span>

    ![選取使用者屬性](./media/active-directory-saas-sapboc-tutorial/config6.png)

13. <span data-ttu-id="e2b53-194">hello 身分識別提供者 (步驟 4)，在 hello tooverify hello 帳戶**登入認證 （電子郵件）**方塊中，輸入 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e2b53-194">tooverify hello account with hello identity provider (Step 4), in hello **Login Credential (Email)** box, enter hello user's email address.</span></span> <span data-ttu-id="e2b53-195">然後，選取 [驗證帳戶]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-195">Then, select **Verify Account**.</span></span> <span data-ttu-id="e2b53-196">hello 系統新增登入認證 toohello 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e2b53-196">hello system adds sign-in credentials toohello user account.</span></span>

    ![輸入電子郵件，並選取 [驗證帳戶]](./media/active-directory-saas-sapboc-tutorial/config7.png)

14. <span data-ttu-id="e2b53-198">選取 hello**儲存**圖示。</span><span class="sxs-lookup"><span data-stu-id="e2b53-198">Select hello **Save** icon.</span></span>

    ![[儲存] 圖示](./media/active-directory-saas-sapboc-tutorial/save.png)

> [!TIP]
> <span data-ttu-id="e2b53-200">您可以讀取這些指示 hello 的精簡版本[Azure 入口網站](https://portal.azure.com)，而您要設定您的應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="e2b53-200">You can read a concise version of these instructions in hello [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="e2b53-201">選取 [新增 hello 應用程式之後**Active Directory** > **企業應用程式**，選取 hello**單一登入**] 索引標籤。您可以存取 hello 內嵌文件以 hello**組態**區段中的，在 hello hello 頁面底部。</span><span class="sxs-lookup"><span data-stu-id="e2b53-201">After you add hello app by selecting **Active Directory** > **Enterprise Applications**, select hello **Single Sign-On** tab. You can access hello embedded documentation in hello **Configuration** section, at hello bottom of hello page.</span></span> <span data-ttu-id="e2b53-202">如需詳細資訊，請參閱 [Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-202">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e2b53-203">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e2b53-203">Create an Azure AD test user</span></span>
<span data-ttu-id="e2b53-204">在本節中，您可以建立 hello Azure 入口網站中名為許 Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="e2b53-204">In this section, you create a test user named Britta Simon in hello Azure portal.</span></span>

<span data-ttu-id="e2b53-205">toocreate 在 Azure AD 中的測試使用者：</span><span class="sxs-lookup"><span data-stu-id="e2b53-205">toocreate a test user in Azure AD:</span></span>

1. <span data-ttu-id="e2b53-206">在 [hello Azure 入口網站，在 hello 左功能表中，選取 [ **Azure Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-206">In hello Azure portal, in hello left menu, select **Azure Active Directory**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2b53-208">toodisplay hello 使用者清單，選取**使用者和群組**，然後選取**所有使用者**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-208">toodisplay hello list of users, select **Users and groups**, and then select **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2b53-210">tooopen hello**使用者**對話方塊中，選取**新增**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-210">tooopen hello **User** dialog box, select **Add**.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-sapboc-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2b53-212">在 [hello**使用者**對話方塊中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e2b53-212">In hello **User** dialog box, complete hello following steps:</span></span>
 
    1. <span data-ttu-id="e2b53-213">在 [hello**名稱**方塊中，輸入**BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-213">In hello **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="e2b53-214">在 [hello**使用者名**方塊中，輸入 hello 使用者許 Simon hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="e2b53-214">In hello **User name** box, enter hello email address of hello user Britta Simon.</span></span>

    3. <span data-ttu-id="e2b53-215">選取 hello**顯示密碼**核取方塊，並寫下 hello 值，會顯示在 [hello**密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="e2b53-215">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    4. <span data-ttu-id="e2b53-216">選取 [ **建立**]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-216">Select **Create**.</span></span>

        ![hello [使用者] 對話方塊](./media/active-directory-saas-sapboc-tutorial/create_aaduser_04.png) 

    ![建立 Azure AD 使用者][100]

### <a name="create-an-sap-business-object-cloud-test-user"></a><span data-ttu-id="e2b53-219">建立 SAP Business Object Cloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e2b53-219">Create an SAP Business Object Cloud test user</span></span>

<span data-ttu-id="e2b53-220">必須 SAP 商務物件雲端中佈建 azure AD 使用者，才可以登入 tooSAP 商務物件的雲端。</span><span class="sxs-lookup"><span data-stu-id="e2b53-220">Azure AD users must be provisioned in SAP Business Object Cloud before they can sign in tooSAP Business Object Cloud.</span></span> <span data-ttu-id="e2b53-221">在 SAP Business Object Cloud 中，必須以手動方式進行佈建。</span><span class="sxs-lookup"><span data-stu-id="e2b53-221">In SAP Business Object Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="e2b53-222">tooprovision 使用者帳戶：</span><span class="sxs-lookup"><span data-stu-id="e2b53-222">tooprovision a user account:</span></span>

1. <span data-ttu-id="e2b53-223">Tooyour SAP 商務物件雲端公司網站管理員身分登入。</span><span class="sxs-lookup"><span data-stu-id="e2b53-223">Sign in tooyour SAP Business Object Cloud company site as an administrator.</span></span>

2. <span data-ttu-id="e2b53-224">選取 [功能表] > [安全性] > [使用者]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-224">Select **Menu** > **Security** > **Users**.</span></span>

    ![新增員工](./media/active-directory-saas-sapboc-tutorial/user1.png)

3. <span data-ttu-id="e2b53-226">在 [hello**使用者**tooadd 新的使用者詳細資料頁面選取** + **。</span><span class="sxs-lookup"><span data-stu-id="e2b53-226">On hello **Users** page, tooadd new user details, select **+**.</span></span> 

    ![新增使用者頁面](./media/active-directory-saas-sapboc-tutorial/user4.png)

    <span data-ttu-id="e2b53-228">接著，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="e2b53-228">Then, complete hello following steps:</span></span>

    1. <span data-ttu-id="e2b53-229">在 [hello**使用者識別碼**方塊中，輸入 hello hello 使用者，使用者識別碼，例如**許**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-229">In hello **USER ID** box, enter hello user ID of hello user, like **Britta**.</span></span>

    2. <span data-ttu-id="e2b53-230">在 [hello**名字**方塊中，例如輸入 hello 使用者 hello 名字**許**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-230">In hello **FIRST NAME** box, enter hello first name of hello user, like **Britta**.</span></span>

    3. <span data-ttu-id="e2b53-231">在 [hello**姓氏**方塊中，輸入 hello 最後一個 hello 使用者名稱，例如**Simon**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-231">In hello **LAST NAME** box, enter hello last name of hello user, like **Simon**.</span></span>

    4. <span data-ttu-id="e2b53-232">在 [hello**顯示名稱**方塊中，輸入 hello 完整 hello 使用者名稱，例如**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-232">In hello **DISPLAY NAME** box, enter hello full name of hello user, like **Britta Simon**.</span></span>

    5. <span data-ttu-id="e2b53-233">在 [hello**電子郵件**方塊中，輸入 hello hello 使用者電子郵件地址，例如** brittasimon@contoso.com **。</span><span class="sxs-lookup"><span data-stu-id="e2b53-233">In hello **E-MAIL** box, enter hello email address of hello user, like **brittasimon@contoso.com**.</span></span>

    6. <span data-ttu-id="e2b53-234">在 [hello**選取角色**頁面上，選取 hello hello 使用者適當的角色，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-234">On hello **Select Roles** page, select hello appropriate role for hello user, and then select **OK**.</span></span>

      ![選取角色](./media/active-directory-saas-sapboc-tutorial/user3.png)

    7. <span data-ttu-id="e2b53-236">選取 hello**儲存**圖示。</span><span class="sxs-lookup"><span data-stu-id="e2b53-236">Select hello **Save** icon.</span></span>  


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e2b53-237">指派給 Azure AD hello 測試使用者</span><span class="sxs-lookup"><span data-stu-id="e2b53-237">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e2b53-238">在本節中，您允許 hello 使用者許 Simon toouse Azure AD 單一登入授與 hello 使用者帳戶存取 tooSAP 商務物件的雲端。</span><span class="sxs-lookup"><span data-stu-id="e2b53-238">In this section, you allow hello user Britta Simon toouse Azure AD single sign-on by granting hello user account access tooSAP Business Object Cloud.</span></span>

<span data-ttu-id="e2b53-239">tooassign 許 Simon tooSAP 商務物件雲端：</span><span class="sxs-lookup"><span data-stu-id="e2b53-239">tooassign Britta Simon tooSAP Business Object Cloud:</span></span>

1. <span data-ttu-id="e2b53-240">在 [hello Azure 入口網站，開啟 hello 應用程式檢視，並前往 toohello 目錄檢視。</span><span class="sxs-lookup"><span data-stu-id="e2b53-240">In hello Azure portal, open hello applications view, and then go toohello directory view.</span></span> <span data-ttu-id="e2b53-241">選取 [企業應用程式]，然後選取 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e2b53-241">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="e2b53-243">在 [hello] 應用程式清單中，選取**SAP 商務物件雲端**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-243">In hello applications list, select **SAP Business Object Cloud**.</span></span>

    ![設定單一登入](./media/active-directory-saas-sapboc-tutorial/tutorial_sapboc_app.png) 

3. <span data-ttu-id="e2b53-245">在 [hello 左窗格中，選取 [**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-245">In hello left menu, select **Users and groups**.</span></span>

    ![選取 [使用者和群組]][202] 

4. <span data-ttu-id="e2b53-247">選取 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="e2b53-247">Select **Add**.</span></span> <span data-ttu-id="e2b53-248">然後，在 hello**將作業加入**頁面上，選取**使用者和群組**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-248">Then, on hello **Add Assignment** page, select **Users and groups**.</span></span>

    ![hello 新增指派] 頁面][203]

5. <span data-ttu-id="e2b53-250">在 [hello**使用者和群組**頁面 hello 清單中的使用者，選取**許 Simon**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-250">On hello **Users and groups** page, in hello list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="e2b53-251">在 [hello**使用者和群組**頁面上，選取**選取**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-251">On hello **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="e2b53-252">在 [hello**將作業加入**頁面上，選取**指派**。</span><span class="sxs-lookup"><span data-stu-id="e2b53-252">On hello **Add Assignment** page, select **Assign**.</span></span>

![指派 hello 使用者角色][200] 
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e2b53-254">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="e2b53-254">Test single sign-on</span></span>

<span data-ttu-id="e2b53-255">在本節中，您測試您 Azure AD 單一登入組態使用 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="e2b53-255">In this section, you test your Azure AD single sign-on configuration by using hello access panel.</span></span>

<span data-ttu-id="e2b53-256">當您選取 hello SAP 商務物件雲端磚 hello 存取面板中時，您應該會自動登入 tooyour SAP 商務物件雲端應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2b53-256">When you select hello SAP Business Object Cloud tile in hello access panel, you should be automatically signed in tooyour SAP Business Object Cloud application.</span></span>

<span data-ttu-id="e2b53-257">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="e2b53-257">For more information about hello access panel, see [Introduction toohello access panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2b53-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="e2b53-258">Additional resources</span></span>

* [<span data-ttu-id="e2b53-259">如何教學課程清單 toointegrate SaaS 應用程式與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2b53-259">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2b53-260">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="e2b53-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapboc-tutorial/tutorial_general_203.png

