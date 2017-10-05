---
title: "教學課程：Azure Active Directory 與 Zoho 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Zoho 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="cf4c7-103">教學課程：Azure Active Directory 與 Zoho 整合</span><span class="sxs-lookup"><span data-stu-id="cf4c7-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="cf4c7-104">在本教學課程中，您會了解如何將 Zoho 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf4c7-105">Zoho 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cf4c7-106">您可以在 Azure AD 中控制可存取 Zoho 的人員。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="cf4c7-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Zoho (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="cf4c7-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="cf4c7-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf4c7-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="cf4c7-110">Prerequisites</span></span>

<span data-ttu-id="cf4c7-111">若要設定 Azure AD 與 Zoho 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="cf4c7-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cf4c7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf4c7-113">已啟用 Zoho 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="cf4c7-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf4c7-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf4c7-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf4c7-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf4c7-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf4c7-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="cf4c7-118">Scenario description</span></span>
<span data-ttu-id="cf4c7-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf4c7-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf4c7-121">從資源庫新增 Zoho</span><span class="sxs-lookup"><span data-stu-id="cf4c7-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="cf4c7-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cf4c7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="cf4c7-123">從資源庫新增 Zoho</span><span class="sxs-lookup"><span data-stu-id="cf4c7-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="cf4c7-124">若要設定將 Zoho 整合到 Azure AD 中，您需要從資源庫將 Zoho 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cf4c7-125">**若要從資源庫加入 Zoho，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cf4c7-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cf4c7-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="cf4c7-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cf4c7-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="cf4c7-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="cf4c7-133">在搜尋方塊中，輸入 **Zoho**，從結果面板中選取 [Zoho]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="cf4c7-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cf4c7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="cf4c7-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Zoho 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf4c7-137">若要讓單一登入運作，Azure AD 必須知道 Zoho 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="cf4c7-138">換句話說，必須建立 Azure AD 使用者和 Zoho 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="cf4c7-139">在 Zoho 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cf4c7-140">若要設定及測試與 Zoho 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cf4c7-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cf4c7-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf4c7-143">**[建立 Zoho 測試使用者](#create-a-zoho-test-user)** - 使 Zoho 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf4c7-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf4c7-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="cf4c7-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="cf4c7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="cf4c7-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Zoho 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="cf4c7-148">**若要使用 Zoho 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cf4c7-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="cf4c7-149">在 Azure 入口網站的 [Zoho] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="cf4c7-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="cf4c7-153">在 [Zoho 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Zoho 網域與 URL 單一登入資訊](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="cf4c7-155">a.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-155">a.</span></span> <span data-ttu-id="cf4c7-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="cf4c7-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf4c7-157">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-157">This value is not real.</span></span> <span data-ttu-id="cf4c7-158">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="cf4c7-159">請連絡 [Zoho 客戶支援小組](https://www.zoho.com/mail/contact.html)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="cf4c7-160">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="cf4c7-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-162">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="cf4c7-164">在 [Zoho 組態] 區段上，按一下 [設定 Zoho] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cf4c7-165">從 [快速參考] 區段中複製「登出 URL」、「變更密碼 URL」及「SAML 單一登入服務 URL」。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Zoho 組態](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="cf4c7-167">在不同的 Web 瀏覽器視窗中，以系統管理員身分登入您的 Zoho Mail 公司網站。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="cf4c7-168">移至 [控制台] 。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="cf4c7-169">![控制台](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "控制台")</span><span class="sxs-lookup"><span data-stu-id="cf4c7-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="cf4c7-170">按一下 [SAML 驗證]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="cf4c7-171">![SAML 驗證](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="cf4c7-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="cf4c7-172">在 [SAML 驗證詳細資料]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="cf4c7-173">![SAML 驗證詳細資料](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML 驗證詳細資料")</span><span class="sxs-lookup"><span data-stu-id="cf4c7-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="cf4c7-174">a.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-174">a.</span></span> <span data-ttu-id="cf4c7-175">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 **SAML 單一登入服務 URL**。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cf4c7-176">b.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-176">b.</span></span> <span data-ttu-id="cf4c7-177">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**登出 URL**。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cf4c7-178">c.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-178">c.</span></span> <span data-ttu-id="cf4c7-179">在 [變更密碼 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [變更密碼 URL]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="cf4c7-180">d.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-180">d.</span></span> <span data-ttu-id="cf4c7-181">在記事本中開啟從 Azure 入口網站下載的 Base-64 編碼憑證，將其內容複製到您的剪貼簿，然後貼到 [PublicKey] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="cf4c7-182">e.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-182">e.</span></span> <span data-ttu-id="cf4c7-183">選取 [RSA] 做為 [演算法]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="cf4c7-184">f.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-184">f.</span></span> <span data-ttu-id="cf4c7-185">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="cf4c7-186">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="cf4c7-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cf4c7-187">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cf4c7-188">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cf4c7-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="cf4c7-189">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cf4c7-189">Create an Azure AD test user</span></span>

<span data-ttu-id="cf4c7-190">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="cf4c7-192">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cf4c7-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cf4c7-193">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="cf4c7-195">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="cf4c7-197">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="cf4c7-199">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-199">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="cf4c7-201">a.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-201">a.</span></span> <span data-ttu-id="cf4c7-202">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf4c7-203">b.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-203">b.</span></span> <span data-ttu-id="cf4c7-204">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="cf4c7-205">c.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-205">c.</span></span> <span data-ttu-id="cf4c7-206">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="cf4c7-207">d.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-207">d.</span></span> <span data-ttu-id="cf4c7-208">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="cf4c7-209">建立 Zoho 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cf4c7-209">Create a Zoho test user</span></span>

<span data-ttu-id="cf4c7-210">若要讓 Azure AD 使用者可以登入 Zoho Mail，必須將他們佈建到 Zoho Mail。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="cf4c7-211">Zoho Mail 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="cf4c7-212">您可以使用任何其他的 Zoho Mail 使用者帳戶建立工具或 Zoho Mail 提供的 API，佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="cf4c7-213">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="cf4c7-214">以系統管理員身分登入您的 **Zoho Mail** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="cf4c7-215">移至 [控制台] \> [郵件和文件]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="cf4c7-216">移至 [使用者詳細資料] \> [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="cf4c7-217">![新增使用者](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="cf4c7-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="cf4c7-218">在 [新增使用者]  對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cf4c7-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="cf4c7-219">![新增使用者](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="cf4c7-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="cf4c7-220">a.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-220">a.</span></span> <span data-ttu-id="cf4c7-221">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="cf4c7-222">b.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-222">b.</span></span> <span data-ttu-id="cf4c7-223">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="cf4c7-224">c.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-224">c.</span></span> <span data-ttu-id="cf4c7-225">在 [電子郵件識別碼] 文字方塊中，輸入像是 **brittasimon@contoso.com** 的使用者電子郵件識別碼。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="cf4c7-226">d.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-226">d.</span></span> <span data-ttu-id="cf4c7-227">在 [密碼] 文字方塊中，輸入使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="cf4c7-228">e.</span><span class="sxs-lookup"><span data-stu-id="cf4c7-228">e.</span></span> <span data-ttu-id="cf4c7-229">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="cf4c7-230">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="cf4c7-231">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="cf4c7-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="cf4c7-232">在本節中，您會將 Zoho 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="cf4c7-234">**若要將 Britta Simon 指派給 Zoho，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="cf4c7-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="cf4c7-235">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="cf4c7-237">在應用程式清單中，選取 [Zoho]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-237">In the applications list, select **Zoho**.</span></span>

    ![應用程式清單中的 Zoho 連結](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="cf4c7-239">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-239">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="cf4c7-241">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-241">Click **Add** button.</span></span> <span data-ttu-id="cf4c7-242">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="cf4c7-244">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cf4c7-245">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf4c7-246">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="cf4c7-247">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="cf4c7-247">Test single sign-on</span></span>

<span data-ttu-id="cf4c7-248">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cf4c7-249">當您在存取面板中按一下 [Zoho] 圖格時，應該會自動登入您的 Zoho 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="cf4c7-250">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="cf4c7-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="cf4c7-251">其他資源</span><span class="sxs-lookup"><span data-stu-id="cf4c7-251">Additional resources</span></span>

* [<span data-ttu-id="cf4c7-252">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="cf4c7-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf4c7-253">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="cf4c7-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

