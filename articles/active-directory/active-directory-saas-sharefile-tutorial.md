---
title: "教學課程：Azure Active Directory 與 Citrix ShareFile 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Citrix ShareFile 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: e14fc310-bac4-4f09-99ef-87e5c77288b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2017
ms.author: jeedes
ms.openlocfilehash: b85680104fe4f33638c559b2a12483a2312a4476
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-sharefile"></a><span data-ttu-id="bdfd4-103">教學課程：Azure Active Directory 與 Citrix ShareFile 整合</span><span class="sxs-lookup"><span data-stu-id="bdfd4-103">Tutorial: Azure Active Directory integration with Citrix ShareFile</span></span>

<span data-ttu-id="bdfd4-104">在本教學課程中，您會了解如何整合 Citrix ShareFile 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-104">In this tutorial, you learn how to integrate Citrix ShareFile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bdfd4-105">Citrix ShareFile 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-105">Integrating Citrix ShareFile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bdfd4-106">您可以在 Azure AD 中控制可存取 Citrix ShareFile 的人員。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-106">You can control in Azure AD who has access to Citrix ShareFile.</span></span>
- <span data-ttu-id="bdfd4-107">您可以讓使用者使用他們的 Azure AD 帳戶，自動登入 Citrix ShareFile (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-107">You can enable your users to automatically get signed-on to Citrix ShareFile (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="bdfd4-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="bdfd4-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdfd4-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="bdfd4-110">Prerequisites</span></span>

<span data-ttu-id="bdfd4-111">若要設定 Azure AD 與 Citrix ShareFile 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-111">To configure Azure AD integration with Citrix ShareFile, you need the following items:</span></span>

- <span data-ttu-id="bdfd4-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bdfd4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bdfd4-113">已啟用 Citrix ShareFile 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bdfd4-113">A Citrix ShareFile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bdfd4-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bdfd4-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bdfd4-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bdfd4-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bdfd4-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="bdfd4-118">Scenario description</span></span>
<span data-ttu-id="bdfd4-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bdfd4-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bdfd4-121">從資源庫新增 Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="bdfd4-121">Add Citrix ShareFile from the gallery</span></span>
2. <span data-ttu-id="bdfd4-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bdfd4-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-citrix-sharefile-from-the-gallery"></a><span data-ttu-id="bdfd4-123">從資源庫新增 Citrix ShareFile</span><span class="sxs-lookup"><span data-stu-id="bdfd4-123">Add Citrix ShareFile from the gallery</span></span>
<span data-ttu-id="bdfd4-124">若要設定 Citrix ShareFile 與 Azure AD 整合，您需要從資源庫將 Citrix ShareFile 新增到受管理的 SaaS App 清單。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-124">To configure the integration of Citrix ShareFile into Azure AD, you need to add Citrix ShareFile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bdfd4-125">**若要從資源庫新增 Citrix ShareFile，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bdfd4-125">**To add Citrix ShareFile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bdfd4-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="bdfd4-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bdfd4-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="bdfd4-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="bdfd4-133">在搜尋方塊中，輸入 **Citrix ShareFile**，從結果面板中選取 **Citrix ShareFile**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-133">In the search box, type **Citrix ShareFile**, select **Citrix ShareFile** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Citrix ShareFile](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="bdfd4-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bdfd4-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="bdfd4-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Citrix ShareFile 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-136">In this section, you configure and test Azure AD single sign-on with Citrix ShareFile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bdfd4-137">若要讓單一登入運作，Azure AD 必須知道 Citrix ShareFile 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Citrix ShareFile is to a user in Azure AD.</span></span> <span data-ttu-id="bdfd4-138">換句話說，必須在 Azure AD 使用者和 Citrix ShareFile 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-138">In other words, a link relationship between an Azure AD user and the related user in Citrix ShareFile needs to be established.</span></span>

<span data-ttu-id="bdfd4-139">在 Citrix ShareFile 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-139">In Citrix ShareFile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bdfd4-140">若要設定及測試與 Citrix ShareFile 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-140">To configure and test Azure AD single sign-on with Citrix ShareFile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bdfd4-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bdfd4-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bdfd4-143">**[建立 Citrix ShareFile 測試使用者](#create-a-citrix-sharefile-test-user)** - 在 Citrix ShareFile 中建立一個與 Azure AD 中代表 Britta Simon 的項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-143">**[Create a Citrix ShareFile test user](#create-a-citrix-sharefile-test-user)** - to have a counterpart of Britta Simon in Citrix ShareFile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bdfd4-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bdfd4-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="bdfd4-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="bdfd4-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="bdfd4-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Citrix ShareFile 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Citrix ShareFile application.</span></span>

<span data-ttu-id="bdfd4-148">**若要使用 Citrix ShareFile 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bdfd4-148">**To configure Azure AD single sign-on with Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="bdfd4-149">在 Azure 入口網站的 [Citrix ShareFile] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-149">In the Azure portal, on the **Citrix ShareFile** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="bdfd4-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_samlbase.png)

3. <span data-ttu-id="bdfd4-153">在 [Citrix ShareFile 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-153">On the **Citrix ShareFile Domain and URLs** section, perform the following steps:</span></span>

    ![Citrix ShareFile 網域與 URL 單一登入資訊](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_url.png)
    
    <span data-ttu-id="bdfd4-155">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.sharefile.com/saml/login`</span><span class="sxs-lookup"><span data-stu-id="bdfd4-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.sharefile.com/saml/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bdfd4-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-156">This value is not real.</span></span> <span data-ttu-id="bdfd4-157">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="bdfd4-158">請連絡 [Citrix ShareFile 用戶端支援小組](https://www.citrix.co.in/products/sharefile/support.html)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-158">Contact [Citrix ShareFile Client support team](https://www.citrix.co.in/products/sharefile/support.html) to get this value.</span></span> 

4. <span data-ttu-id="bdfd4-159">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-159">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_certificate.png) 

5. <span data-ttu-id="bdfd4-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-sharefile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bdfd4-163">在 [Citrix ShareFile 設定] 區段中，按一下 [設定 Citrix ShareFile] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-163">On the **Citrix ShareFile Configuration** section, click **Configure Citrix ShareFile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="bdfd4-164">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Citrix ShareFile 設定](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_configure.png) 

7. <span data-ttu-id="bdfd4-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 **Citrix ShareFile** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-166">In a different web browser window, log into your **Citrix ShareFile** company site as an administrator.</span></span>

8. <span data-ttu-id="bdfd4-167">在頂端工具列中，按一下 [管理] 。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-167">In the toolbar on the top, click **Admin**.</span></span>

9. <span data-ttu-id="bdfd4-168">在左側瀏覽窗格中，選取 [設定單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-168">In the left navigation pane, select **Configure Single Sign-On**.</span></span>
   
    <span data-ttu-id="bdfd4-169">![帳戶管理](./media/active-directory-saas-sharefile-tutorial/ic773627.png "帳戶管理")</span><span class="sxs-lookup"><span data-stu-id="bdfd4-169">![Account Administration](./media/active-directory-saas-sharefile-tutorial/ic773627.png "Account Administration")</span></span>

10. <span data-ttu-id="bdfd4-170">在 [單一登入/SAML 2.0 組態] 對話頁面的 [基本設定] 下方，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-170">On the **Single Sign-On/ SAML 2.0 Configuration** dialog page under **Basic Settings**, perform the following steps:</span></span>
   
    <span data-ttu-id="bdfd4-171">![單一登入](./media/active-directory-saas-sharefile-tutorial/ic773628.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="bdfd4-171">![Single sign-on](./media/active-directory-saas-sharefile-tutorial/ic773628.png "Single sign-on")</span></span>
   
    <span data-ttu-id="bdfd4-172">a.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-172">a.</span></span> <span data-ttu-id="bdfd4-173">按一下 [啟用 SAML] 。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-173">Click **Enable SAML**.</span></span>
    
    <span data-ttu-id="bdfd4-174">b.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-174">b.</span></span> <span data-ttu-id="bdfd4-175">在 [您的 IDP 簽發者/實體識別碼] 文字方塊中，貼上從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-175">In **Your IDP Issuer/ Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="bdfd4-176">c.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-176">c.</span></span> <span data-ttu-id="bdfd4-177">按一下 [X.509 憑證] 欄位旁的 [變更]，然後上傳您從 Azure 入口網站下載的憑證。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-177">Click **Change** next to the **X.509 Certificate** field and then upload the certificate you downloaded from the Azure portal.</span></span>
    
    <span data-ttu-id="bdfd4-178">d.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-178">d.</span></span> <span data-ttu-id="bdfd4-179">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-179">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="bdfd4-180">e.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-180">e.</span></span> <span data-ttu-id="bdfd4-181">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-181">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

11. <span data-ttu-id="bdfd4-182">在 Citrix ShareFile 管理入口網站上，按一下 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-182">Click **Save** on the Citrix ShareFile management portal.</span></span>

> [!TIP]
> <span data-ttu-id="bdfd4-183">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="bdfd4-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bdfd4-184">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bdfd4-185">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bdfd4-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="bdfd4-186">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bdfd4-186">Create an Azure AD test user</span></span>

<span data-ttu-id="bdfd4-187">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="bdfd4-189">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bdfd4-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bdfd4-190">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-sharefile-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="bdfd4-192">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-sharefile-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="bdfd4-194">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-sharefile-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="bdfd4-196">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-196">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-sharefile-tutorial/create_aaduser_04.png)

    <span data-ttu-id="bdfd4-198">a.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-198">a.</span></span> <span data-ttu-id="bdfd4-199">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bdfd4-200">b.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-200">b.</span></span> <span data-ttu-id="bdfd4-201">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="bdfd4-202">c.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-202">c.</span></span> <span data-ttu-id="bdfd4-203">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="bdfd4-204">d.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-204">d.</span></span> <span data-ttu-id="bdfd4-205">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-205">Click **Create**.</span></span>
 
### <a name="create-a-citrix-sharefile-test-user"></a><span data-ttu-id="bdfd4-206">建立 Citrix ShareFile 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bdfd4-206">Create a Citrix ShareFile test user</span></span>

<span data-ttu-id="bdfd4-207">若要讓 Azure AD 使用者可以登入 Citrix ShareFile，必須將他們佈建到 Citrix ShareFile。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-207">In order to enable Azure AD users to log into Citrix ShareFile, they must be provisioned into Citrix ShareFile.</span></span> <span data-ttu-id="bdfd4-208">Citrix ShareFile 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-208">In the case of Citrix ShareFile, provisioning is a manual task.</span></span>

<span data-ttu-id="bdfd4-209">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bdfd4-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="bdfd4-210">登入您的 **Citrix ShareFile** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-210">Log in to your **Citrix ShareFile** tenant.</span></span>

2. <span data-ttu-id="bdfd4-211">按一下 [管理使用者] \> [管理使用者首頁] \> [+ 建立員工]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-211">Click **Manage Users \> Manage Users Home \> + Create Employee**.</span></span>
   
   <span data-ttu-id="bdfd4-212">![建立員工](./media/active-directory-saas-sharefile-tutorial/IC781050.png "建立員工")</span><span class="sxs-lookup"><span data-stu-id="bdfd4-212">![Create Employee](./media/active-directory-saas-sharefile-tutorial/IC781050.png "Create Employee")</span></span>

3. <span data-ttu-id="bdfd4-213">在 [基本資訊] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="bdfd4-213">On the **Basic Information** section, perform below steps:</span></span>
   
   <span data-ttu-id="bdfd4-214">![基本資訊](./media/active-directory-saas-sharefile-tutorial/IC799951.png "的基本資訊")</span><span class="sxs-lookup"><span data-stu-id="bdfd4-214">![Basic Information](./media/active-directory-saas-sharefile-tutorial/IC799951.png "Basic Information")</span></span>
   
   <span data-ttu-id="bdfd4-215">a.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-215">a.</span></span> <span data-ttu-id="bdfd4-216">在 [電子郵件地址] 文字方塊中，將 Britta Simon 的電子郵件地址輸入為 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-216">In the **Email Address** textbox, type the email address of Britta Simon as **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="bdfd4-217">b.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-217">b.</span></span> <span data-ttu-id="bdfd4-218">在 [名字] 文字方塊中，輸入 **Britta** 作為使用者的**名字**。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-218">In the **First Name** textbox, type **first name** of user as **Britta**.</span></span>
   
   <span data-ttu-id="bdfd4-219">c.</span><span class="sxs-lookup"><span data-stu-id="bdfd4-219">c.</span></span> <span data-ttu-id="bdfd4-220">在 [姓氏] 文字方塊中，輸入 **Simon** 作為使用者的**姓氏**。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-220">In the **Last Name** textbox, type **last name** of user as **Simon**.</span></span>

4. <span data-ttu-id="bdfd4-221">按一下 [加入使用者] 。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-221">Click **Add User**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="bdfd4-222">Azure AD 帳戶持有者將收到一封電子郵件，依循連結來確認其帳戶，帳戶就會生效。您可以使用任何其他 Citrix ShareFile 使用者帳戶建立工具或 Citrix ShareFile 所提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-222">The Azure AD account holder will receive an email and follow a link to confirm their account before it becomes active.You can use any other Citrix ShareFile user account creation tools or APIs provided by Citrix ShareFile to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="bdfd4-223">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="bdfd4-223">Assign the Azure AD test user</span></span>

<span data-ttu-id="bdfd4-224">在本節中，您會將 Citrix ShareFile 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Citrix ShareFile.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="bdfd4-226">**若要將 Britta Simon 指派給 Citrix ShareFile，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="bdfd4-226">**To assign Britta Simon to Citrix ShareFile, perform the following steps:**</span></span>

1. <span data-ttu-id="bdfd4-227">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="bdfd4-229">在應用程式清單中，選取 [Citrix ShareFile]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-229">In the applications list, select **Citrix ShareFile**.</span></span>

    ![應用程式清單中的 Citrix ShareFile 連結](./media/active-directory-saas-sharefile-tutorial/tutorial_sharefile_app.png)  

3. <span data-ttu-id="bdfd4-231">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-231">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="bdfd4-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-233">Click **Add** button.</span></span> <span data-ttu-id="bdfd4-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="bdfd4-236">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bdfd4-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bdfd4-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="bdfd4-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="bdfd4-239">Test single sign-on</span></span>

<span data-ttu-id="bdfd4-240">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bdfd4-241">當您在存取面板中按一下 [Citrix ShareFile] 圖格時，應該會自動登入您的 Citrix ShareFile 應用程式。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-241">When you click the Citrix ShareFile tile in the Access Panel, you should get automatically signed-on to your Citrix ShareFile application.</span></span>
<span data-ttu-id="bdfd4-242">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="bdfd4-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bdfd4-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="bdfd4-243">Additional resources</span></span>

* [<span data-ttu-id="bdfd4-244">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="bdfd4-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bdfd4-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="bdfd4-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sharefile-tutorial/tutorial_general_203.png

