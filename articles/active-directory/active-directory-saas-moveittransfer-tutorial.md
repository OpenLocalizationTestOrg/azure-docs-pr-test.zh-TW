---
title: "教學課程：Azure Active Directory 與 MOVEit Transfer - Azure AD integration 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 MOVEit Transfer - Azure AD integration 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: d35aceb9be2d0ff49f86a00cc84f5deb198d88f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a><span data-ttu-id="87bdb-103">教學課程：Azure Active Directory 與 MOVEit Transfer - Azure AD integration 整合</span><span class="sxs-lookup"><span data-stu-id="87bdb-103">Tutorial: Azure Active Directory integration with MOVEit Transfer - Azure AD integration</span></span>

<span data-ttu-id="87bdb-104">在本教學課程中，您將了解如何整合 MOVEit Transfer - Azure AD integration 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="87bdb-104">In this tutorial, you learn how to integrate MOVEit Transfer - Azure AD integration with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87bdb-105">將 MOVEit Transfer - Azure AD integration 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="87bdb-105">Integrating MOVEit Transfer - Azure AD integration with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="87bdb-106">您可以在 Azure AD 中控制可存取 MOVEit Transfer - Azure AD integration 的人員。</span><span class="sxs-lookup"><span data-stu-id="87bdb-106">You can control in Azure AD who has access to MOVEit Transfer - Azure AD integration.</span></span>
- <span data-ttu-id="87bdb-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 MOVEit Transfer - Azure AD integration (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="87bdb-107">You can enable your users to automatically get signed-on to MOVEit Transfer - Azure AD integration (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="87bdb-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="87bdb-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="87bdb-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="87bdb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87bdb-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="87bdb-110">Prerequisites</span></span>

<span data-ttu-id="87bdb-111">若要設定 Azure AD 與 MOVEit Transfer - Azure AD integration 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="87bdb-111">To configure Azure AD integration with MOVEit Transfer - Azure AD integration, you need the following items:</span></span>

- <span data-ttu-id="87bdb-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="87bdb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87bdb-113">已啟用 MOVEit Transfer - Azure AD integration 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="87bdb-113">A MOVEit Transfer - Azure AD integration single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87bdb-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="87bdb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87bdb-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="87bdb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87bdb-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="87bdb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87bdb-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="87bdb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87bdb-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="87bdb-118">Scenario description</span></span>
<span data-ttu-id="87bdb-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87bdb-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="87bdb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87bdb-121">從資源庫新增 MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="87bdb-121">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
2. <span data-ttu-id="87bdb-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="87bdb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-moveit-transfer---azure-ad-integration-from-the-gallery"></a><span data-ttu-id="87bdb-123">從資源庫新增 MOVEit Transfer - Azure AD integration</span><span class="sxs-lookup"><span data-stu-id="87bdb-123">Adding MOVEit Transfer - Azure AD integration from the gallery</span></span>
<span data-ttu-id="87bdb-124">若要設定 MOVEit Transfer - Azure AD integration 與 Azure AD 整合，您需要從資源庫將 MOVEit Transfer - Azure AD integration 新增到受管理的 SaaS 應用程式清單中。</span><span class="sxs-lookup"><span data-stu-id="87bdb-124">To configure the integration of MOVEit Transfer - Azure AD integration into Azure AD, you need to add MOVEit Transfer - Azure AD integration from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="87bdb-125">**若要從資源庫新增 MOVEit Transfer - Azure AD integration，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="87bdb-125">**To add MOVEit Transfer - Azure AD integration from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="87bdb-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="87bdb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="87bdb-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="87bdb-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="87bdb-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="87bdb-133">在搜尋方塊中，輸入 **MOVEit Transfer - Azure AD integration**，從結果面板中選取 [MOVEit Transfer - Azure AD integration]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="87bdb-133">In the search box, type **MOVEit Transfer - Azure AD integration**, select **MOVEit Transfer - Azure AD integration** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 MOVEit Transfer - Azure AD integration](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="87bdb-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="87bdb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="87bdb-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 MOVEit Transfer - Azure AD integration 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-136">In this section, you configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="87bdb-137">若要讓單一登入運作，Azure AD 必須知道 MOVEit Transfer - Azure AD integration 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="87bdb-137">For single sign-on to work, Azure AD needs to know what the counterpart user in MOVEit Transfer - Azure AD integration is to a user in Azure AD.</span></span> <span data-ttu-id="87bdb-138">換句話說，必須建立 Azure AD 使用者和 MOVEit Transfer - Azure AD integration 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="87bdb-138">In other words, a link relationship between an Azure AD user and the related user in MOVEit Transfer - Azure AD integration needs to be established.</span></span>

<span data-ttu-id="87bdb-139">在 MOVEit Transfer - Azure AD integration 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="87bdb-139">In MOVEit Transfer - Azure AD integration, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="87bdb-140">若要設定及測試對 MOVEit Transfer - Azure AD integration 的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="87bdb-140">To configure and test Azure AD single sign-on with MOVEit Transfer - Azure AD integration, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="87bdb-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="87bdb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="87bdb-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87bdb-143">**[建立 MOVEit Transfer - Azure AD integration 測試使用者](#create-a-moveit-transfer---azure-ad-integration-test-user)** - 使 MOVEit Transfer - Azure AD integration 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="87bdb-143">**[Create a MOVEit Transfer - Azure AD integration test user](#create-a-moveit-transfer---azure-ad-integration-test-user)** - to have a counterpart of Britta Simon in MOVEit Transfer - Azure AD integration that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="87bdb-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87bdb-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="87bdb-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="87bdb-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="87bdb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="87bdb-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，並在您的 MOVEit Transfer - Azure AD integration 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MOVEit Transfer - Azure AD integration application.</span></span>

<span data-ttu-id="87bdb-148">**若要使用 MOVEit Transfer - Azure AD integration 設定 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="87bdb-148">**To configure Azure AD single sign-on with MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="87bdb-149">在 Azure 入口網站的 [MOVEit Transfer - Azure AD integration] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-149">In the Azure portal, on the **MOVEit Transfer - Azure AD integration** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="87bdb-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. <span data-ttu-id="87bdb-153">在 [MOVEit Transfer - Azure AD integration 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="87bdb-153">On the **MOVEit Transfer - Azure AD integration Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    <span data-ttu-id="87bdb-155">a.</span><span class="sxs-lookup"><span data-stu-id="87bdb-155">a.</span></span> <span data-ttu-id="87bdb-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://contoso.com`</span><span class="sxs-lookup"><span data-stu-id="87bdb-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://contoso.com`</span></span>

    <span data-ttu-id="87bdb-157">b.</span><span class="sxs-lookup"><span data-stu-id="87bdb-157">b.</span></span> <span data-ttu-id="87bdb-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://contoso.com/<tenatid>`</span><span class="sxs-lookup"><span data-stu-id="87bdb-158">In the **Identifier** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>`</span></span>

    <span data-ttu-id="87bdb-159">c.</span><span class="sxs-lookup"><span data-stu-id="87bdb-159">c.</span></span> <span data-ttu-id="87bdb-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span><span class="sxs-lookup"><span data-stu-id="87bdb-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="87bdb-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="87bdb-161">These values are not real.</span></span> <span data-ttu-id="87bdb-162">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="87bdb-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="87bdb-163">您可以稍後在 [服務提供者中繼資料 URL] 區段中參照這些值，或連絡 [MOVEit Transfer - Azure AD integration 用戶端支援小組](https://community.ipswitch.com/s/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="87bdb-163">You can refer these values later in **Service Provider Metadata URL** section or contact [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support) to get these values.</span></span>

4. <span data-ttu-id="87bdb-164">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="87bdb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. <span data-ttu-id="87bdb-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-166">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="87bdb-168">以系統管理員身分登入 MOVEit Transfer 租用戶。</span><span class="sxs-lookup"><span data-stu-id="87bdb-168">Sign on to your MOVEit Transfer tenant as an administrator.</span></span>

7. <span data-ttu-id="87bdb-169">在左側的導覽窗格上，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="87bdb-169">On the left navigation pane, click **Settings**.</span></span>

    ![應用程式端上的設定區段](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. <span data-ttu-id="87bdb-171">按一下 [單一登入] 連結，其位於 [安全性原則] -> [使用者驗證] 下。</span><span class="sxs-lookup"><span data-stu-id="87bdb-171">Click **Single Signon** link, which is under **Security Policies -> User Auth**.</span></span>

    ![應用程式端上的安全性原則](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. <span data-ttu-id="87bdb-173">按一下 [中繼資料 URL] 連結以下載中繼資料文件。</span><span class="sxs-lookup"><span data-stu-id="87bdb-173">Click the Metadata URL link to download the metadata document.</span></span>

    ![服務提供者中繼資料 URL](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * <span data-ttu-id="87bdb-175">確認 **entityID** 符合 [MOVEit Transfer - Azure AD integration 網域與 URL] 區段中的 [識別碼]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-175">Verify **entityID** matches **Identifier** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section .</span></span>
    * <span data-ttu-id="87bdb-176">確認 **AssertionConsumerService** 位置 URL 符合 [MOVEit Transfer - Azure AD integration 網域與 URL] 區段中的 [回覆 URL]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-176">Verify **AssertionConsumerService** Location URL matches **REPLY URL** in the **MOVEit Transfer - Azure AD integration Domain and URLs** section.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. <span data-ttu-id="87bdb-178">按一下 [新增識別提供者]  按鈕來加入新的同盟識別提供者。</span><span class="sxs-lookup"><span data-stu-id="87bdb-178">Click **Add Identity Provider** button to add a new Federated Identity Provider.</span></span>

    ![新增識別提供者](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. <span data-ttu-id="87bdb-180">按一下 [瀏覽...] 以選取您從 Azure 入口網站下載的中繼資料檔案，然後按一下 [新增識別提供者] 以上傳所下載的檔案。</span><span class="sxs-lookup"><span data-stu-id="87bdb-180">Click **Browse...** to select the metadata file which you downloaded from Azure portal, then click **Add Identity Provider** to upload the downloaded file.</span></span>

    ![SAML 識別提供者](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. <span data-ttu-id="87bdb-182">選取 [是] 做為 [編輯同盟識別提供者設定...] 頁面中的 [啟用]，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-182">Select "**Yes**" as **Enabled** in the **Edit Federated Identity Provider Settings...** page and click **Save**.</span></span>

    ![同盟識別提供者設定](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. <span data-ttu-id="87bdb-184">在 [編輯同盟識別提供者使用者設定] 頁面中，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="87bdb-184">In the **Edit Federated Identity Provider User Settings** page, perform the following actions:</span></span>
    
    ![編輯同盟識別提供者設定](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    <span data-ttu-id="87bdb-186">a.</span><span class="sxs-lookup"><span data-stu-id="87bdb-186">a.</span></span> <span data-ttu-id="87bdb-187">選取 [SAML NameID] 做為 [登入名稱]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-187">Select **SAML NameID** as **Login name**.</span></span>
    
    <span data-ttu-id="87bdb-188">b.</span><span class="sxs-lookup"><span data-stu-id="87bdb-188">b.</span></span> <span data-ttu-id="87bdb-189">在 [其他] 中選取 [全名]，並在 [屬性名稱] 文字方塊中，輸入值：`http://schemas.microsoft.com/identity/claims/displayname`。</span><span class="sxs-lookup"><span data-stu-id="87bdb-189">Select **Other** as **Full name** and in the **Attribute name** textbox put the value: `http://schemas.microsoft.com/identity/claims/displayname`.</span></span>
    
    <span data-ttu-id="87bdb-190">c.</span><span class="sxs-lookup"><span data-stu-id="87bdb-190">c.</span></span> <span data-ttu-id="87bdb-191">在 [其他] 中選取 [電子郵件]，並在 [屬性名稱] 文字方塊中，輸入值：`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="87bdb-191">Select **Other** as **Email** and in the **Attribute name** textbox put the value: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="87bdb-192">d.</span><span class="sxs-lookup"><span data-stu-id="87bdb-192">d.</span></span> <span data-ttu-id="87bdb-193">選取 [是] 做為 [在登入時自動建立帳戶]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-193">Select **Yes** as **Auto-create account on signon**.</span></span>
    
    <span data-ttu-id="87bdb-194">e.</span><span class="sxs-lookup"><span data-stu-id="87bdb-194">e.</span></span> <span data-ttu-id="87bdb-195">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-195">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="87bdb-196">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="87bdb-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="87bdb-197">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="87bdb-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="87bdb-198">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87bdb-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="87bdb-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="87bdb-199">Create an Azure AD test user</span></span>

<span data-ttu-id="87bdb-200">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="87bdb-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="87bdb-202">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="87bdb-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="87bdb-203">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-203">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="87bdb-205">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-205">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="87bdb-207">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-207">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="87bdb-209">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="87bdb-209">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    <span data-ttu-id="87bdb-211">a.</span><span class="sxs-lookup"><span data-stu-id="87bdb-211">a.</span></span> <span data-ttu-id="87bdb-212">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="87bdb-212">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87bdb-213">b.</span><span class="sxs-lookup"><span data-stu-id="87bdb-213">b.</span></span> <span data-ttu-id="87bdb-214">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="87bdb-214">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="87bdb-215">c.</span><span class="sxs-lookup"><span data-stu-id="87bdb-215">c.</span></span> <span data-ttu-id="87bdb-216">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="87bdb-216">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="87bdb-217">d.</span><span class="sxs-lookup"><span data-stu-id="87bdb-217">d.</span></span> <span data-ttu-id="87bdb-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="87bdb-218">Click **Create**.</span></span>
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a><span data-ttu-id="87bdb-219">建立 MOVEit Transfer - Azure AD integration 測試使用者</span><span class="sxs-lookup"><span data-stu-id="87bdb-219">Create a MOVEit Transfer - Azure AD integration test user</span></span>

<span data-ttu-id="87bdb-220">本節的目標是要在 MOVEit Transfer - Azure AD integration 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="87bdb-220">The objective of this section is to create a user called Britta Simon in MOVEit Transfer - Azure AD integration.</span></span> <span data-ttu-id="87bdb-221">MOVEit Transfer - Azure AD integration 支援您已啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="87bdb-221">MOVEit Transfer - Azure AD integration supports just-in-time provisioning, which you have enabled.</span></span> <span data-ttu-id="87bdb-222">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="87bdb-222">There is no action item for you in this section.</span></span> <span data-ttu-id="87bdb-223">嘗試存取 MOVEit Transfer - Azure AD integration 時若尚無使用者，則會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="87bdb-223">A new user is created during an attempt to access MOVEit Transfer - Azure AD integration if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="87bdb-224">如果您需要手動建立使用者，則必須連絡 [MOVEit Transfer - Azure AD integration 用戶端支援小組](https://community.ipswitch.com/s/support)。</span><span class="sxs-lookup"><span data-stu-id="87bdb-224">If you need to create a user manually, you need to contact the [MOVEit Transfer - Azure AD integration Client support team](https://community.ipswitch.com/s/support).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="87bdb-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="87bdb-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="87bdb-226">在本節中，您會將 MOVEit Transfer - Azure AD integration 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="87bdb-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MOVEit Transfer - Azure AD integration.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="87bdb-228">**如要將 Britta Simon 指派給 MOVEit Transfer - Azure AD integration，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="87bdb-228">**To assign Britta Simon to MOVEit Transfer - Azure AD integration, perform the following steps:**</span></span>

1. <span data-ttu-id="87bdb-229">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="87bdb-231">在應用程式清單中，選取 [MOVEit Transfer - Azure AD integration]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-231">In the applications list, select **MOVEit Transfer - Azure AD integration**.</span></span>

    ![應用程式清單中的 MOVEit Transfer - Azure AD integration 連結](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. <span data-ttu-id="87bdb-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-233">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="87bdb-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-235">Click **Add** button.</span></span> <span data-ttu-id="87bdb-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="87bdb-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="87bdb-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="87bdb-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87bdb-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="87bdb-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="87bdb-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="87bdb-241">Test single sign-on</span></span>

<span data-ttu-id="87bdb-242">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="87bdb-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="87bdb-243">當您在「存取面板」中按一下 [MOVEit Transfer - Azure AD integration] 圖格時，應該會自動登入您的 MOVEit Transfer - Azure AD integration 應用程式。</span><span class="sxs-lookup"><span data-stu-id="87bdb-243">When you click the MOVEit Transfer - Azure AD integration tile in the Access Panel, you should get automatically signed-on to your MOVEit Transfer - Azure AD integration application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="87bdb-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="87bdb-244">Additional resources</span></span>

* [<span data-ttu-id="87bdb-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="87bdb-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87bdb-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="87bdb-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

