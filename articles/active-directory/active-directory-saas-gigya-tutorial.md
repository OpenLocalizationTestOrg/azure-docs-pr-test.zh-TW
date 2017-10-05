---
title: "教學課程：Azure Active Directory 與 Gigya 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Gigya 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2c7d200b-9242-44a5-ac8a-ab3214a78e41
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: b65a33989a045a3e0b57fda522a9bc3b0770c7f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gigya"></a><span data-ttu-id="f9878-103">教學課程：Azure Active Directory 與 Gigya 整合</span><span class="sxs-lookup"><span data-stu-id="f9878-103">Tutorial: Azure Active Directory integration with Gigya</span></span>

<span data-ttu-id="f9878-104">在本教學課程中，您將了解如何整合 Gigya 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="f9878-104">In this tutorial, you learn how to integrate Gigya with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9878-105">Gigya 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f9878-105">Integrating Gigya with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9878-106">您可以在 Azure AD 中控制可存取 Gigya 的人員</span><span class="sxs-lookup"><span data-stu-id="f9878-106">You can control in Azure AD who has access to Gigya</span></span>
- <span data-ttu-id="f9878-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Gigya (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f9878-107">You can enable your users to automatically get signed-on to Gigya (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9878-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f9878-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9878-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f9878-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9878-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f9878-110">Prerequisites</span></span>

<span data-ttu-id="f9878-111">若要設定 Azure AD 與 Gigya 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f9878-111">To configure Azure AD integration with Gigya, you need the following items:</span></span>

- <span data-ttu-id="f9878-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f9878-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9878-113">已啟用 Gigya 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f9878-113">A Gigya single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9878-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f9878-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9878-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f9878-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9878-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f9878-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9878-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f9878-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9878-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="f9878-118">Scenario description</span></span>
<span data-ttu-id="f9878-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9878-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f9878-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9878-121">從資源庫新增 Gigya</span><span class="sxs-lookup"><span data-stu-id="f9878-121">Adding Gigya from the gallery</span></span>
2. <span data-ttu-id="f9878-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f9878-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gigya-from-the-gallery"></a><span data-ttu-id="f9878-123">從資源庫新增 Gigya</span><span class="sxs-lookup"><span data-stu-id="f9878-123">Adding Gigya from the gallery</span></span>
<span data-ttu-id="f9878-124">若要設定將 Gigya 整合到 Azure AD 中，您需要從資源庫將 Gigya 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f9878-124">To configure the integration of Gigya into Azure AD, you need to add Gigya from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9878-125">**若要從資源庫新增 Gigya，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f9878-125">**To add Gigya from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9878-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f9878-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9878-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f9878-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9878-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f9878-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f9878-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9878-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f9878-133">在搜尋方塊中，輸入 **Gigya**。</span><span class="sxs-lookup"><span data-stu-id="f9878-133">In the search box, type **Gigya**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_search.png)

5. <span data-ttu-id="f9878-135">在結果窗格中，選取 [Gigya]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9878-135">In the results panel, select **Gigya**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9878-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f9878-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9878-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Gigya 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-138">In this section, you configure and test Azure AD single sign-on with Gigya based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f9878-139">若要讓單一登入運作，Azure AD 必須知道 Gigya 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f9878-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Gigya is to a user in Azure AD.</span></span> <span data-ttu-id="f9878-140">換句話說，必須建立 Azure AD 使用者和 Gigya 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f9878-140">In other words, a link relationship between an Azure AD user and the related user in Gigya needs to be established.</span></span>

<span data-ttu-id="f9878-141">在 Gigya 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f9878-141">In Gigya, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9878-142">若要設定及測試與 Gigya 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="f9878-142">To configure and test Azure AD single sign-on with Gigya, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9878-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f9878-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9878-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9878-145">**[建立 Gigya 測試使用者](#creating-a-gigya-test-user)** - 在 Gigya 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="f9878-145">**[Creating a Gigya test user](#creating-a-gigya-test-user)** - to have a counterpart of Britta Simon in Gigya that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9878-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f9878-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9878-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f9878-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9878-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Gigya 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Gigya application.</span></span>

<span data-ttu-id="f9878-150">**若要使用 Gigya 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f9878-150">**To configure Azure AD single sign-on with Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="f9878-151">在 Azure 入口網站的 [Gigya] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="f9878-151">In the Azure portal, on the **Gigya** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f9878-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_samlbase.png)

3. <span data-ttu-id="f9878-155">在 [Gigya 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f9878-155">On the **Gigya Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_url.png)

    <span data-ttu-id="f9878-157">a.</span><span class="sxs-lookup"><span data-stu-id="f9878-157">a.</span></span> <span data-ttu-id="f9878-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`http://<companyname>.gigya.com`</span><span class="sxs-lookup"><span data-stu-id="f9878-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<companyname>.gigya.com`</span></span>

    <span data-ttu-id="f9878-159">b.</span><span class="sxs-lookup"><span data-stu-id="f9878-159">b.</span></span> <span data-ttu-id="f9878-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://fidm.gigya.com/saml/v2.0/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="f9878-160">In the **Identifier** textbox, type a URL using the following pattern: `https://fidm.gigya.com/saml/v2.0/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9878-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="f9878-161">These values are not real.</span></span> <span data-ttu-id="f9878-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="f9878-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f9878-163">請連絡 [Gigya 用戶端支援小組](https://www.gigya.com/support-policy/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="f9878-163">Contact [Gigya Client support team](https://www.gigya.com/support-policy/) to get these values.</span></span> 
 
4. <span data-ttu-id="f9878-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f9878-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_certificate.png) 

5. <span data-ttu-id="f9878-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9878-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f9878-168">在 [Gigya 組態] 區段上，按一下 [設定 Gigya] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="f9878-168">On the **Gigya Configuration** section, click **Configure Gigya** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f9878-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="f9878-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_configure.png) 

7. <span data-ttu-id="f9878-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Gigya 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f9878-171">In a different web browser window, log into your Gigya company site as an administrator.</span></span>

8. <span data-ttu-id="f9878-172">移至 [設定]\>[SAML 登入]，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9878-172">Go to **Settings \> SAML Login**, and then click the **Add** button.</span></span>
   
    <span data-ttu-id="f9878-173">![SAML 登入](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML 登入")</span><span class="sxs-lookup"><span data-stu-id="f9878-173">![SAML Login](./media/active-directory-saas-gigya-tutorial/ic789532.png "SAML Login")</span></span>

9. <span data-ttu-id="f9878-174">在 [SAML 登入]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f9878-174">In the **SAML Login** section, perform the following steps:</span></span>
   
    <span data-ttu-id="f9878-175">![SAML 設定](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML 設定")</span><span class="sxs-lookup"><span data-stu-id="f9878-175">![SAML Configuration](./media/active-directory-saas-gigya-tutorial/ic789533.png "SAML Configuration")</span></span>
   
    <span data-ttu-id="f9878-176">a.</span><span class="sxs-lookup"><span data-stu-id="f9878-176">a.</span></span> <span data-ttu-id="f9878-177">在 [名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="f9878-177">In the **Name** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="f9878-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9878-178">b.</span></span> <span data-ttu-id="f9878-179">在 [簽發者] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 實體識別碼] 值。</span><span class="sxs-lookup"><span data-stu-id="f9878-179">In **Issuer** textbox, paste the value of **SAML Entity ID** which you have copied from Azure Portal.</span></span> 
   
    <span data-ttu-id="f9878-180">c.</span><span class="sxs-lookup"><span data-stu-id="f9878-180">c.</span></span> <span data-ttu-id="f9878-181">在 [單一登入服務 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="f9878-181">In **Single Sign-On Service URL** textbox, paste the value of **Single Sign-On Service URL** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="f9878-182">d.</span><span class="sxs-lookup"><span data-stu-id="f9878-182">d.</span></span> <span data-ttu-id="f9878-183">在 [名稱識別碼格式] 文字方塊中，貼上您從 Azure 入口網站複製的 [名稱識別碼格式] 值。</span><span class="sxs-lookup"><span data-stu-id="f9878-183">In **Name ID Format** textbox, paste the value of **Name Identifier Format** which you have copied from Azure Portal.</span></span>
   
    <span data-ttu-id="f9878-184">e.</span><span class="sxs-lookup"><span data-stu-id="f9878-184">e.</span></span> <span data-ttu-id="f9878-185">在從 Azure 入口網站下載的記事本檔案中開啟您的 base-64 編碼憑證，將憑證的內容複製到剪貼簿，再貼到 [X.509 憑證] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f9878-185">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="f9878-186">f.</span><span class="sxs-lookup"><span data-stu-id="f9878-186">f.</span></span> <span data-ttu-id="f9878-187">按一下 [儲存設定] 。</span><span class="sxs-lookup"><span data-stu-id="f9878-187">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="f9878-188">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f9878-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9878-189">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f9878-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9878-190">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f9878-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9878-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f9878-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="f9878-192">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f9878-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f9878-194">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f9878-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9878-195">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f9878-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9878-197">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f9878-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9878-199">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f9878-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9878-201">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f9878-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-gigya-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9878-203">a.</span><span class="sxs-lookup"><span data-stu-id="f9878-203">a.</span></span> <span data-ttu-id="f9878-204">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f9878-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9878-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9878-205">b.</span></span> <span data-ttu-id="f9878-206">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f9878-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9878-207">c.</span><span class="sxs-lookup"><span data-stu-id="f9878-207">c.</span></span> <span data-ttu-id="f9878-208">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f9878-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9878-209">d.</span><span class="sxs-lookup"><span data-stu-id="f9878-209">d.</span></span> <span data-ttu-id="f9878-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f9878-210">Click **Create**.</span></span>
 
### <a name="creating-a-gigya-test-user"></a><span data-ttu-id="f9878-211">建立 Gigya 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f9878-211">Creating a Gigya test user</span></span>

<span data-ttu-id="f9878-212">若要讓 Azure AD 使用者可以登入 Gigya，則必須將他們佈建到 Gigya。</span><span class="sxs-lookup"><span data-stu-id="f9878-212">In order to enable Azure AD users to log into Gigya, they must be provisioned into Gigya.</span></span>  
<span data-ttu-id="f9878-213">Gigya 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="f9878-213">In the case of Gigya, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="f9878-214">若要佈建使用者帳戶，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f9878-214">To provision a user accounts, perform the following steps:</span></span>

1. <span data-ttu-id="f9878-215">以系統管理員身分登入您的 **Gigya** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="f9878-215">Log in to your **Gigya** company site as an administrator.</span></span>

2. <span data-ttu-id="f9878-216">移至 [系統管理員]\>[管理使用者]，然後按一下 [邀請使用者]。</span><span class="sxs-lookup"><span data-stu-id="f9878-216">Go to **Admin \> Manage Users**, and then click **Invite Users**.</span></span>
   
    <span data-ttu-id="f9878-217">![管理使用者](./media/active-directory-saas-gigya-tutorial/ic789535.png "管理使用者")</span><span class="sxs-lookup"><span data-stu-id="f9878-217">![Manage Users](./media/active-directory-saas-gigya-tutorial/ic789535.png "Manage Users")</span></span>

3. <span data-ttu-id="f9878-218">在 [邀請使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f9878-218">On the Invite Users dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="f9878-219">![邀請使用者](./media/active-directory-saas-gigya-tutorial/ic789536.png "邀請使用者")</span><span class="sxs-lookup"><span data-stu-id="f9878-219">![Invite Users](./media/active-directory-saas-gigya-tutorial/ic789536.png "Invite Users")</span></span>
   
    <span data-ttu-id="f9878-220">a.</span><span class="sxs-lookup"><span data-stu-id="f9878-220">a.</span></span> <span data-ttu-id="f9878-221">在 [電子郵件]  文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的電子郵件別名。</span><span class="sxs-lookup"><span data-stu-id="f9878-221">In the **Email** textbox, type the email alias of a valid Azure Active Directory account you want to provision.</span></span>
    
    <span data-ttu-id="f9878-222">b.</span><span class="sxs-lookup"><span data-stu-id="f9878-222">b.</span></span> <span data-ttu-id="f9878-223">按一下 [邀請使用者] 。</span><span class="sxs-lookup"><span data-stu-id="f9878-223">Click **Invite User**.</span></span>
      
    > [!NOTE]
    > <span data-ttu-id="f9878-224">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="f9878-224">The Azure Active Directory account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span>
    > 
    

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9878-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f9878-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9878-226">在本節中，您會將 Gigya 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f9878-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Gigya.</span></span>

![指派使用者][200] 

<span data-ttu-id="f9878-228">**若要將 Britta Simon 指派給 Gigya，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f9878-228">**To assign Britta Simon to Gigya, perform the following steps:**</span></span>

1. <span data-ttu-id="f9878-229">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f9878-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f9878-231">在應用程式清單中，選取 [Gigya] 。</span><span class="sxs-lookup"><span data-stu-id="f9878-231">In the applications list, select **Gigya**.</span></span>

    ![設定單一登入](./media/active-directory-saas-gigya-tutorial/tutorial_gigya_app.png) 

3. <span data-ttu-id="f9878-233">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f9878-233">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f9878-235">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9878-235">Click **Add** button.</span></span> <span data-ttu-id="f9878-236">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f9878-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f9878-238">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f9878-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9878-239">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9878-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9878-240">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f9878-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9878-241">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f9878-241">Testing single sign-on</span></span>

<span data-ttu-id="f9878-242">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="f9878-242">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="f9878-243">當您在存取面板中按一下 Gigya 圖格時，應該會自動登入您的 Gigya 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f9878-243">When you click the Gigya tile in the Access Panel, you should get automatically signed-on to your Gigya application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9878-244">其他資源</span><span class="sxs-lookup"><span data-stu-id="f9878-244">Additional resources</span></span>

* [<span data-ttu-id="f9878-245">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f9878-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9878-246">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f9878-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gigya-tutorial/tutorial_general_203.png

