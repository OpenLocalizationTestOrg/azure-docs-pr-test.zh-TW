---
title: "教學課程：Azure Active Directory 與 Voyance 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Voyance 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 539dc1f9-64c9-4dce-b259-2b0b49dcf857
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2017
ms.author: jeedes
ms.openlocfilehash: e860b810904fb7972d75d55d913d5622ff9a406a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-voyance"></a><span data-ttu-id="b0d10-103">教學課程：Azure Active Directory 與 Voyance 整合</span><span class="sxs-lookup"><span data-stu-id="b0d10-103">Tutorial: Azure Active Directory integration with Voyance</span></span>

<span data-ttu-id="b0d10-104">在本教學課程中，您將了解如何整合 Voyance 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b0d10-104">In this tutorial, you learn how to integrate Voyance with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0d10-105">Voyance 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b0d10-105">Integrating Voyance with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b0d10-106">您可以在 Azure AD 中控制可存取 Voyance 的人員</span><span class="sxs-lookup"><span data-stu-id="b0d10-106">You can control in Azure AD who has access to Voyance</span></span>
- <span data-ttu-id="b0d10-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Voyance (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b0d10-107">You can enable your users to automatically get signed-on to Voyance (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0d10-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b0d10-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b0d10-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b0d10-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0d10-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b0d10-110">Prerequisites</span></span>

<span data-ttu-id="b0d10-111">若要設定 Azure AD 與 Voyance 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b0d10-111">To configure Azure AD integration with Voyance, you need the following items:</span></span>

- <span data-ttu-id="b0d10-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b0d10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0d10-113">已啟用 Voyance 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b0d10-113">A Voyance single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0d10-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b0d10-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0d10-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b0d10-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0d10-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b0d10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0d10-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b0d10-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0d10-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b0d10-118">Scenario description</span></span>
<span data-ttu-id="b0d10-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0d10-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b0d10-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0d10-121">從資源庫新增 Voyance</span><span class="sxs-lookup"><span data-stu-id="b0d10-121">Adding Voyance from the gallery</span></span>
2. <span data-ttu-id="b0d10-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b0d10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-voyance-from-the-gallery"></a><span data-ttu-id="b0d10-123">從資源庫新增 Voyance</span><span class="sxs-lookup"><span data-stu-id="b0d10-123">Adding Voyance from the gallery</span></span>
<span data-ttu-id="b0d10-124">若要設定 Voyance 與 Azure AD 整合，您需要從資源庫將 Voyance 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b0d10-124">To configure the integration of Voyance into Azure AD, you need to add Voyance from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0d10-125">**若要從資源庫新增 Voyance，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b0d10-125">**To add Voyance from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0d10-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b0d10-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="b0d10-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b0d10-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="b0d10-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0d10-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="b0d10-133">在搜尋方塊中，輸入 **Voyance**，從結果面板中選取 **Voyance**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0d10-133">In the search box, type **Voyance**, select  **Voyance**  from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Voyance](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b0d10-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b0d10-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="b0d10-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Voyance 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-136">In this section, you configure and test Azure AD single sign-on with Voyance based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0d10-137">若要讓單一登入運作，Azure AD 必須知道 Voyance 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b0d10-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Voyance is to a user in Azure AD.</span></span> <span data-ttu-id="b0d10-138">換句話說，必須建立 Azure AD 使用者和 Voyance 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b0d10-138">In other words, a link relationship between an Azure AD user and the related user in Voyance needs to be established.</span></span>

<span data-ttu-id="b0d10-139">在 Voyance 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b0d10-139">In Voyance, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b0d10-140">若要設定及測試與 Voyance 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="b0d10-140">To configure and test Azure AD single sign-on with Voyance, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0d10-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b0d10-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0d10-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0d10-143">**[建立 Voyance 測試使用者](#create-a-voyance-test-user)** - 讓 Voyance 中對應的 Britta Simon 連結到使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b0d10-143">**[Create a Voyance test user](#create-a-voyance-test-user)** - to have a counterpart of Britta Simon in Voyance that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0d10-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0d10-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b0d10-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b0d10-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b0d10-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b0d10-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Voyance 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Voyance application.</span></span>

<span data-ttu-id="b0d10-148">**若要設定與 Voyance 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b0d10-148">**To configure Azure AD single sign-on with Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="b0d10-149">在 Azure 入口網站的 [Voyance] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-149">In the Azure portal, on the **Voyance** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="b0d10-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_samlbase.png)

3. <span data-ttu-id="b0d10-153">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Voyance 網域和 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b0d10-153">On the **Voyance Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![IDP 的 Voyance 網域和 URL 單一登入資訊](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url1.png)

    <span data-ttu-id="b0d10-155">a.</span><span class="sxs-lookup"><span data-stu-id="b0d10-155">a.</span></span> <span data-ttu-id="b0d10-156">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.nyansa.com`</span><span class="sxs-lookup"><span data-stu-id="b0d10-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com`</span></span>

    <span data-ttu-id="b0d10-157">b.</span><span class="sxs-lookup"><span data-stu-id="b0d10-157">b.</span></span> <span data-ttu-id="b0d10-158">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.nyansa.com/saml/create/`</span><span class="sxs-lookup"><span data-stu-id="b0d10-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/saml/create/`</span></span>

4. <span data-ttu-id="b0d10-159">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]，然後執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b0d10-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![SP 的 Voyance 網域和 URL 單一登入資訊](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_url2.png)

    <span data-ttu-id="b0d10-161">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.nyansa.com/`</span><span class="sxs-lookup"><span data-stu-id="b0d10-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.nyansa.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="b0d10-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b0d10-162">These values are not real.</span></span> <span data-ttu-id="b0d10-163">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="b0d10-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="b0d10-164">請連絡 [Voyance 客戶支援小組](mailto:support@nyansa.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="b0d10-164">Contact [Voyance Client support team](mailto:support@nyansa.com) to get these values.</span></span> 

5. <span data-ttu-id="b0d10-165">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b0d10-165">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_certificate.png) 

6. <span data-ttu-id="b0d10-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0d10-167">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-voyance-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="b0d10-169">在 [Voyance 組態] 區段上，按一下 [設定 Voyance] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b0d10-169">On the **Voyance Configuration** section, click **Configure Voyance** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b0d10-170">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-170">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Voyance 組態](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_configure.png) 

8. <span data-ttu-id="b0d10-172">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 Voyance 租用戶。</span><span class="sxs-lookup"><span data-stu-id="b0d10-172">In a different web browser window, sign-on to your Voyance tenant as an administrator.</span></span>

9. <span data-ttu-id="b0d10-173">移至瀏覽列右上角，然後按一下 [Acme 大學]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-173">Go to the top right corner of the navigation bar and click on the drop-down that says "**Acme University**".</span></span>
    
    ![在應用程式端設定單一登入 Acme 大學](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_001.png) 

10. <span data-ttu-id="b0d10-175">按一下 [系統管理員設定]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-175">Click "**Admin Settings**".</span></span>

    ![在應用程式端設定單一登入 系統管理員設定](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_002.png)

11. <span data-ttu-id="b0d10-177">按一下 [使用者存取] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b0d10-177">Click "**User Access**" tab.</span></span>

    ![在應用程式端設定單一登入 使用者存取](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_003.png)

12. <span data-ttu-id="b0d10-179">按一下 [已停用 SSO] 按鈕，將 Azure AD 設定為使用 SAML 2.0 的 IdP。</span><span class="sxs-lookup"><span data-stu-id="b0d10-179">Click the "**SSO is disabled**" button to configure Azure AD as an IdP using SAML 2.0.</span></span>

    ![在應用程式端設定單一登入 [SSO 已停用] 按鈕](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_004.png)

13. <span data-ttu-id="b0d10-181">移至 [SAML v2] 區段並執行下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="b0d10-181">Go to **SAML v2** section and perform below steps:</span></span>

    ![在應用程式端設定單一登入 SAML v2](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_005.png)
    
    <span data-ttu-id="b0d10-183">a.</span><span class="sxs-lookup"><span data-stu-id="b0d10-183">a.</span></span> <span data-ttu-id="b0d10-184">選取 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="b0d10-184">Select **Enabled**.</span></span>
    
    <span data-ttu-id="b0d10-185">b.</span><span class="sxs-lookup"><span data-stu-id="b0d10-185">b.</span></span> <span data-ttu-id="b0d10-186">將您從 Azure 入口網站複製的「SAML 單一登入服務 URL」貼到 [IdP 登入 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b0d10-186">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal Into the **IdP Login URL** textbox.</span></span>

    <span data-ttu-id="b0d10-187">c.</span><span class="sxs-lookup"><span data-stu-id="b0d10-187">c.</span></span> <span data-ttu-id="b0d10-188">在記事本中開啟您下載的 Base64 編碼的憑證，將其內容複製到剪貼簿，然後貼到 [IdP 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b0d10-188">Open your downloaded Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Cert** textbox.</span></span>
    
    <span data-ttu-id="b0d10-189">d.</span><span class="sxs-lookup"><span data-stu-id="b0d10-189">d.</span></span> <span data-ttu-id="b0d10-190">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b0d10-190">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b0d10-191">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b0d10-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b0d10-192">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b0d10-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b0d10-193">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b0d10-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b0d10-194">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b0d10-194">Create an Azure AD test user</span></span>

<span data-ttu-id="b0d10-195">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b0d10-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 測試使用者][100]

<span data-ttu-id="b0d10-197">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b0d10-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0d10-198">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b0d10-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-voyance-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0d10-200">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-voyance-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0d10-202">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-voyance-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0d10-204">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b0d10-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 對話方塊](./media/active-directory-saas-voyance-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0d10-206">a.</span><span class="sxs-lookup"><span data-stu-id="b0d10-206">a.</span></span> <span data-ttu-id="b0d10-207">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b0d10-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0d10-208">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0d10-208">b.</span></span> <span data-ttu-id="b0d10-209">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b0d10-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0d10-210">c.</span><span class="sxs-lookup"><span data-stu-id="b0d10-210">c.</span></span> <span data-ttu-id="b0d10-211">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b0d10-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b0d10-212">d.</span><span class="sxs-lookup"><span data-stu-id="b0d10-212">d.</span></span> <span data-ttu-id="b0d10-213">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b0d10-213">Click **Create**.</span></span>
 
### <a name="create-a-voyance-test-user"></a><span data-ttu-id="b0d10-214">建立 Voyance 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b0d10-214">Create a Voyance test user</span></span>

<span data-ttu-id="b0d10-215">本節的目標是要在 Voyance 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b0d10-215">The objective of this section is to create a user called Britta Simon in Voyance.</span></span> <span data-ttu-id="b0d10-216">Voyance 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="b0d10-216">Voyance supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="b0d10-217">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="b0d10-217">There is no action item for you in this section.</span></span> <span data-ttu-id="b0d10-218">嘗試存取 Voyance 時，如果使用者還不存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="b0d10-218">A new user is created during an attempt to access Voyance if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="b0d10-219">如果您需要手動建立使用者，就必須連絡 [Voyance 支援小組](maiLto:support@nyansa.com)。</span><span class="sxs-lookup"><span data-stu-id="b0d10-219">If you need to create a user manually, you need to contact [Voyance support team](maiLto:support@nyansa.com).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b0d10-220">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b0d10-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="b0d10-221">在本節中，您會將 Voyance 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b0d10-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Voyance.</span></span>

![指派使用者角色][200]

<span data-ttu-id="b0d10-223">**若要將 Britta Simon 指派給 Voyance，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b0d10-223">**To assign Britta Simon to Voyance, perform the following steps:**</span></span>

1. <span data-ttu-id="b0d10-224">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b0d10-226">在應用程式清單中，選取 [Voyance]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-226">In the applications list, select **Voyance**.</span></span>

    ![應用程式清單中的 Voyance 連結](./media/active-directory-saas-voyance-tutorial/tutorial_voyance_app.png) 

3. <span data-ttu-id="b0d10-228">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-228">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="b0d10-230">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0d10-230">Click **Add** button.</span></span> <span data-ttu-id="b0d10-231">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="b0d10-233">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b0d10-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b0d10-234">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0d10-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0d10-235">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b0d10-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b0d10-236">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b0d10-236">Test single sign-on</span></span>

<span data-ttu-id="b0d10-237">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="b0d10-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b0d10-238">當您在存取面板中按一下 Voyance 圖格時，應該會自動登入您的 Voyance 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b0d10-238">When you click the Voyance tile in the Access Panel, you should get automatically signed-on to your Voyance application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0d10-239">其他資源</span><span class="sxs-lookup"><span data-stu-id="b0d10-239">Additional resources</span></span>

* [<span data-ttu-id="b0d10-240">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b0d10-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0d10-241">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b0d10-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-voyance-tutorial/tutorial_general_203.png

