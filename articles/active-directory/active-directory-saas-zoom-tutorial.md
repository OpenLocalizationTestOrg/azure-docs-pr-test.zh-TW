---
title: "教學課程：Azure Active Directory 與 Zoom 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Zoom 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0ebdab6c-83a8-4737-a86a-974f37269c31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: aab491f162fd4d24c6ff4d8858f2edd96dda30d4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoom"></a><span data-ttu-id="4965c-103">教學課程：Azure Active Directory 與 Zoom 整合</span><span class="sxs-lookup"><span data-stu-id="4965c-103">Tutorial: Azure Active Directory integration with Zoom</span></span>

<span data-ttu-id="4965c-104">在本教學課程中，您將了解如何整合 Zoom 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4965c-104">In this tutorial, you learn how to integrate Zoom with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4965c-105">Zoom 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4965c-105">Integrating Zoom with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4965c-106">您可以在 Azure AD 中控制可存取 Zoom 的人員。</span><span class="sxs-lookup"><span data-stu-id="4965c-106">You can control in Azure AD who has access to Zoom.</span></span>
- <span data-ttu-id="4965c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Zoom (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="4965c-107">You can enable your users to automatically get signed-on to Zoom (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4965c-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4965c-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4965c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4965c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4965c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4965c-110">Prerequisites</span></span>

<span data-ttu-id="4965c-111">若要設定 Azure AD 與 Zoom 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4965c-111">To configure Azure AD integration with Zoom, you need the following items:</span></span>

- <span data-ttu-id="4965c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4965c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4965c-113">已啟用 Zoom 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4965c-113">A Zoom single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4965c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4965c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4965c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4965c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4965c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4965c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4965c-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4965c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4965c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4965c-118">Scenario description</span></span>
<span data-ttu-id="4965c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4965c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4965c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4965c-121">從資源庫新增 Zoom</span><span class="sxs-lookup"><span data-stu-id="4965c-121">Adding Zoom from the gallery</span></span>
2. <span data-ttu-id="4965c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4965c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoom-from-the-gallery"></a><span data-ttu-id="4965c-123">從資源庫新增 Zoom</span><span class="sxs-lookup"><span data-stu-id="4965c-123">Adding Zoom from the gallery</span></span>
<span data-ttu-id="4965c-124">若要設定將 Zoom 整合到 Azure AD 中，您需要從資源庫將 Zoom 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="4965c-124">To configure the integration of Zoom into Azure AD, you need to add Zoom from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4965c-125">**若要從資源庫新增 Zoom，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4965c-125">**To add Zoom from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4965c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4965c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="4965c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4965c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4965c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4965c-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="4965c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4965c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="4965c-133">在搜尋方塊中，輸入 **Zoom**，從結果面板中選取 [Zoom]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4965c-133">In the search box, type **Zoom**, select **Zoom** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Zoom](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4965c-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4965c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4965c-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Zoom 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-136">In this section, you configure and test Azure AD single sign-on with Zoom based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4965c-137">若要讓單一登入運作，Azure AD 必須知道 Zoom 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4965c-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoom is to a user in Azure AD.</span></span> <span data-ttu-id="4965c-138">換句話說，必須建立 Azure AD 使用者和 Zoom 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4965c-138">In other words, a link relationship between an Azure AD user and the related user in Zoom needs to be established.</span></span>

<span data-ttu-id="4965c-139">在 Zoom 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4965c-139">In Zoom, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4965c-140">若要設定及測試與 Zoom 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="4965c-140">To configure and test Azure AD single sign-on with Zoom, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4965c-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4965c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4965c-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4965c-143">**[建立 Zoom 測試使用者](#create-a-zoom-test-user)** - 使 Zoom 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="4965c-143">**[Create a Zoom test user](#create-a-zoom-test-user)** - to have a counterpart of Britta Simon in Zoom that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4965c-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4965c-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="4965c-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4965c-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4965c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4965c-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Zoom 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoom application.</span></span>

<span data-ttu-id="4965c-148">**若要使用 Zoom 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4965c-148">**To configure Azure AD single sign-on with Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="4965c-149">在 Azure 入口網站的 [Zoom] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4965c-149">In the Azure portal, on the **Zoom** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="4965c-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_samlbase.png)

3. <span data-ttu-id="4965c-153">在 [Zoom 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4965c-153">On the **Zoom Domain and URLs** section, perform the following steps:</span></span>

    ![Zoom 網域與 URL 單一登入資訊](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_url.png)

    <span data-ttu-id="4965c-155">a.</span><span class="sxs-lookup"><span data-stu-id="4965c-155">a.</span></span> <span data-ttu-id="4965c-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="4965c-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    <span data-ttu-id="4965c-157">b.</span><span class="sxs-lookup"><span data-stu-id="4965c-157">b.</span></span> <span data-ttu-id="4965c-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.zoom.us`</span><span class="sxs-lookup"><span data-stu-id="4965c-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.zoom.us`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4965c-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4965c-159">These values are not real.</span></span> <span data-ttu-id="4965c-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4965c-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4965c-161">請連絡 [Zoom 客戶支援小組](https://support.zoom.us/hc)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="4965c-161">Contact [Zoom Client support team](https://support.zoom.us/hc) to get these values.</span></span> 
 
4. <span data-ttu-id="4965c-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4965c-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_certificate.png) 

5. <span data-ttu-id="4965c-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4965c-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-zoom-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4965c-166">在 [Zoom 組態] 區段上，按一下 [設定 Zoom] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4965c-166">On the **Zoom Configuration** section, click **Configure Zoom** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4965c-167">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4965c-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoom 組態](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_configure.png) 

7. <span data-ttu-id="4965c-169">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zoom 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4965c-169">In a different web browser window, log in to your Zoom company site as an administrator.</span></span>

8. <span data-ttu-id="4965c-170">按一下 [單一登入]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4965c-170">Click the **Single Sign-On** tab.</span></span>
   
    <span data-ttu-id="4965c-171">![[單一登入] 索引標籤](./media/active-directory-saas-zoom-tutorial/IC784700.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="4965c-171">![Single sign-on tab](./media/active-directory-saas-zoom-tutorial/IC784700.png "Single sign-on")</span></span>

9. <span data-ttu-id="4965c-172">按一下 [安全性控制] 索引標籤，然後移至 [單一登入] 設定。</span><span class="sxs-lookup"><span data-stu-id="4965c-172">Click the **Security Control** tab, and then go to the **Single Sign-On** settings.</span></span>

10. <span data-ttu-id="4965c-173">在 [單一登入] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4965c-173">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="4965c-174">![[單一登入] 區段](./media/active-directory-saas-zoom-tutorial/IC784701.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="4965c-174">![Single sign-on section](./media/active-directory-saas-zoom-tutorial/IC784701.png "Single sign-on")</span></span>
   
    <span data-ttu-id="4965c-175">a.</span><span class="sxs-lookup"><span data-stu-id="4965c-175">a.</span></span> <span data-ttu-id="4965c-176">在 [登入頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="4965c-176">In the **Sign-in page URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="4965c-177">b.</span><span class="sxs-lookup"><span data-stu-id="4965c-177">b.</span></span> <span data-ttu-id="4965c-178">在 [登出頁面 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="4965c-178">In the **Sign-out page URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
     
    <span data-ttu-id="4965c-179">c.</span><span class="sxs-lookup"><span data-stu-id="4965c-179">c.</span></span> <span data-ttu-id="4965c-180">在記事本中開啟您的 base-64 編碼的憑證，將其內容複製到您的剪貼簿，然後貼到 [識別提供者憑證]  文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="4965c-180">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Identity provider certificate** textbox.</span></span>

    <span data-ttu-id="4965c-181">d.</span><span class="sxs-lookup"><span data-stu-id="4965c-181">d.</span></span> <span data-ttu-id="4965c-182">在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="4965c-182">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="4965c-183">e.</span><span class="sxs-lookup"><span data-stu-id="4965c-183">e.</span></span> <span data-ttu-id="4965c-184">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4965c-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4965c-185">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="4965c-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4965c-186">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4965c-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4965c-187">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4965c-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4965c-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4965c-188">Create an Azure AD test user</span></span>

<span data-ttu-id="4965c-189">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4965c-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="4965c-191">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4965c-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4965c-192">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4965c-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-zoom-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4965c-194">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4965c-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-zoom-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4965c-196">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4965c-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-zoom-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4965c-198">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4965c-198">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-zoom-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4965c-200">a.</span><span class="sxs-lookup"><span data-stu-id="4965c-200">a.</span></span> <span data-ttu-id="4965c-201">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4965c-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4965c-202">b.</span><span class="sxs-lookup"><span data-stu-id="4965c-202">b.</span></span> <span data-ttu-id="4965c-203">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="4965c-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4965c-204">c.</span><span class="sxs-lookup"><span data-stu-id="4965c-204">c.</span></span> <span data-ttu-id="4965c-205">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="4965c-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4965c-206">d.</span><span class="sxs-lookup"><span data-stu-id="4965c-206">d.</span></span> <span data-ttu-id="4965c-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4965c-207">Click **Create**.</span></span>
 
### <a name="create-a-zoom-test-user"></a><span data-ttu-id="4965c-208">建立 Zoom 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4965c-208">Create a Zoom test user</span></span>

<span data-ttu-id="4965c-209">若要讓 Azure AD 使用者可以登入 Zoom，必須將他們佈建到 Zoom。</span><span class="sxs-lookup"><span data-stu-id="4965c-209">In order to enable Azure AD users to log in to Zoom, they must be provisioned into Zoom.</span></span> <span data-ttu-id="4965c-210">Zoom 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="4965c-210">In the case of Zoom, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="4965c-211">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4965c-211">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="4965c-212">以系統管理員身分登入您的 **Zoom** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4965c-212">Log in to your **Zoom** company site as an administrator.</span></span>
 
2. <span data-ttu-id="4965c-213">按一下 [帳戶管理] 索引標籤，再按一下 [使用者管理]。</span><span class="sxs-lookup"><span data-stu-id="4965c-213">Click the **Account Management** tab, and then click **User Management**.</span></span>

3. <span data-ttu-id="4965c-214">在 [使用者管理] 區段中按一下 [新增使用者] 。</span><span class="sxs-lookup"><span data-stu-id="4965c-214">In the User Management section, click **Add users**.</span></span>
   
    <span data-ttu-id="4965c-215">![使用者管理](./media/active-directory-saas-zoom-tutorial/IC784703.png "使用者管理")</span><span class="sxs-lookup"><span data-stu-id="4965c-215">![User management](./media/active-directory-saas-zoom-tutorial/IC784703.png "User management")</span></span>

4. <span data-ttu-id="4965c-216">在 [新增使用者]  頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4965c-216">On the **Add users** page, perform the following steps:</span></span>
   
    <span data-ttu-id="4965c-217">![新增使用者](./media/active-directory-saas-zoom-tutorial/IC784704.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="4965c-217">![Add users](./media/active-directory-saas-zoom-tutorial/IC784704.png "Add users")</span></span>
   
    <span data-ttu-id="4965c-218">a.</span><span class="sxs-lookup"><span data-stu-id="4965c-218">a.</span></span> <span data-ttu-id="4965c-219">選取 [基本] 做為 [使用者類型]。</span><span class="sxs-lookup"><span data-stu-id="4965c-219">As **User Type**, select **Basic**.</span></span>

    <span data-ttu-id="4965c-220">b.</span><span class="sxs-lookup"><span data-stu-id="4965c-220">b.</span></span> <span data-ttu-id="4965c-221">在 [電子郵件]  文字方塊中，輸入您要佈建之有效 Azure AD 帳戶的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="4965c-221">In the **Emails** textbox, type the email address of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="4965c-222">c.</span><span class="sxs-lookup"><span data-stu-id="4965c-222">c.</span></span> <span data-ttu-id="4965c-223">按一下 [新增] 。</span><span class="sxs-lookup"><span data-stu-id="4965c-223">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="4965c-224">您可以使用任何其他的 Zoom 使用者帳戶建立工具，或 Zoom 提供的 API，以佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4965c-224">You can use any other Zoom user account creation tools or APIs provided by Zoom to provision Azure Active Directory user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4965c-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4965c-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="4965c-226">在本節中，您會將 Zoom 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4965c-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoom.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="4965c-228">**若要將 Britta Simon 指派給 Zoom，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4965c-228">**To assign Britta Simon to Zoom, perform the following steps:**</span></span>

1. <span data-ttu-id="4965c-229">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4965c-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4965c-231">在應用程式清單中，選取 [Zoom]。</span><span class="sxs-lookup"><span data-stu-id="4965c-231">In the applications list, select **Zoom**.</span></span>

    ![應用程式清單中的 Zoom 連結](./media/active-directory-saas-zoom-tutorial/tutorial_zoom_app.png)  

3. <span data-ttu-id="4965c-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4965c-233">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="4965c-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4965c-235">Click **Add** button.</span></span> <span data-ttu-id="4965c-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4965c-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="4965c-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4965c-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4965c-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4965c-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4965c-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4965c-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4965c-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4965c-241">Test single sign-on</span></span>

<span data-ttu-id="4965c-242">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="4965c-242">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4965c-243">當您在存取面板中按一下 [Zoom] 圖格時，應該會自動登入您的 Zoom 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4965c-243">When you click the Zoom tile in the Access Panel, you should get automatically signed-on to your Zoom application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4965c-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="4965c-244">Additional resources</span></span>

* [<span data-ttu-id="4965c-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4965c-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4965c-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4965c-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoom-tutorial/tutorial_general_203.png

