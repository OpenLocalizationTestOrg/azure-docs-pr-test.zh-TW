---
title: "教學課程：Azure Active Directory 與 Bime 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Bime 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 8f46ff1265d302ab114747b4b45227e58718166b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="92dff-103">教學課程：Azure Active Directory 與 Bime 整合</span><span class="sxs-lookup"><span data-stu-id="92dff-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="92dff-104">在本教學課程中，您會了解如何整合 Bime 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="92dff-104">In this tutorial, you learn how to integrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="92dff-105">Bime 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="92dff-105">Integrating Bime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="92dff-106">您可以在 Azure AD 中控制可存取 Bime 的人員</span><span class="sxs-lookup"><span data-stu-id="92dff-106">You can control in Azure AD who has access to Bime</span></span>
- <span data-ttu-id="92dff-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Bime (單一登入)</span><span class="sxs-lookup"><span data-stu-id="92dff-107">You can enable your users to automatically get signed-on to Bime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="92dff-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="92dff-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="92dff-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="92dff-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92dff-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="92dff-110">Prerequisites</span></span>

<span data-ttu-id="92dff-111">若要設定 Azure AD 與 Bime 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="92dff-111">To configure Azure AD integration with Bime, you need the following items:</span></span>

- <span data-ttu-id="92dff-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="92dff-112">An Azure AD subscription</span></span>
- <span data-ttu-id="92dff-113">已啟用 Bime 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="92dff-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="92dff-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="92dff-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="92dff-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="92dff-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="92dff-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="92dff-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="92dff-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="92dff-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="92dff-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="92dff-118">Scenario description</span></span>
<span data-ttu-id="92dff-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="92dff-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="92dff-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="92dff-121">從資源庫新增 Bime</span><span class="sxs-lookup"><span data-stu-id="92dff-121">Adding Bime from the gallery</span></span>
2. <span data-ttu-id="92dff-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="92dff-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-the-gallery"></a><span data-ttu-id="92dff-123">從資源庫新增 Bime</span><span class="sxs-lookup"><span data-stu-id="92dff-123">Adding Bime from the gallery</span></span>
<span data-ttu-id="92dff-124">若要設定將 Bime 整合到 Azure AD 中，您需要從資源庫將 Bime 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="92dff-124">To configure the integration of Bime into Azure AD, you need to add Bime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="92dff-125">**若要從資源庫新增 Bime，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="92dff-125">**To add Bime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="92dff-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="92dff-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="92dff-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="92dff-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="92dff-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="92dff-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="92dff-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92dff-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="92dff-133">在搜尋方塊中，輸入 **Bime**。</span><span class="sxs-lookup"><span data-stu-id="92dff-133">In the search box, type **Bime**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="92dff-135">在結果窗格中，選取 [Bime]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="92dff-135">In the results panel, select **Bime**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="92dff-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="92dff-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="92dff-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Bime 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="92dff-139">若要讓單一登入運作，Azure AD 必須知道 Bime 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="92dff-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bime is to a user in Azure AD.</span></span> <span data-ttu-id="92dff-140">換句話說，必須建立 Azure AD 使用者和 Bime 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="92dff-140">In other words, a link relationship between an Azure AD user and the related user in Bime needs to be established.</span></span>

<span data-ttu-id="92dff-141">在 Bime 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="92dff-141">In Bime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="92dff-142">若要設定及測試與 Bime 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="92dff-142">To configure and test Azure AD single sign-on with Bime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="92dff-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="92dff-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="92dff-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="92dff-145">**[建立 Bime 測試使用者](#creating-a-bime-test-user)** - 在 Bime 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="92dff-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - to have a counterpart of Britta Simon in Bime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="92dff-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="92dff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="92dff-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="92dff-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="92dff-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="92dff-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Bime 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="92dff-150">**若要使用 Bime 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="92dff-150">**To configure Azure AD single sign-on with Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="92dff-151">在 Azure 入口網站的 [Bime] 應用程式整合分頁上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="92dff-151">In the Azure portal, on the **Bime** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="92dff-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="92dff-155">在 [Bime 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="92dff-155">On the **Bime Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="92dff-157">a.</span><span class="sxs-lookup"><span data-stu-id="92dff-157">a.</span></span> <span data-ttu-id="92dff-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="92dff-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="92dff-159">b.</span><span class="sxs-lookup"><span data-stu-id="92dff-159">b.</span></span> <span data-ttu-id="92dff-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="92dff-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="92dff-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="92dff-161">These values are not real.</span></span> <span data-ttu-id="92dff-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="92dff-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="92dff-163">請連絡 [Bime 用戶端支援小組](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="92dff-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) to get these values.</span></span> 
 
4. <span data-ttu-id="92dff-164">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="92dff-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="92dff-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="92dff-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="92dff-168">在 [Bime 設定] 區段上，按一下 [設定 Bime] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="92dff-168">On the **Bime Configuration** section, click **Configure Bime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="92dff-169">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="92dff-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="92dff-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Bime 公司網站。</span><span class="sxs-lookup"><span data-stu-id="92dff-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="92dff-172">在工具列中，按一下 [管理]，然後按一下 [帳戶]。</span><span class="sxs-lookup"><span data-stu-id="92dff-172">In the toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="92dff-173">![管理](./media/active-directory-saas-bime-tutorial/ic775558.png "管理")</span><span class="sxs-lookup"><span data-stu-id="92dff-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="92dff-174">在 [帳戶組態] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="92dff-174">On the account configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="92dff-175">![設定單一登入](./media/active-directory-saas-bime-tutorial/ic775559.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="92dff-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="92dff-176">a.</span><span class="sxs-lookup"><span data-stu-id="92dff-176">a.</span></span> <span data-ttu-id="92dff-177">選取 [啟用 SAML 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="92dff-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="92dff-178">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="92dff-178">b.</span></span> <span data-ttu-id="92dff-179">在 [遠端登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。</span><span class="sxs-lookup"><span data-stu-id="92dff-179">In the **Remote Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="92dff-180">c.</span><span class="sxs-lookup"><span data-stu-id="92dff-180">c.</span></span>  <span data-ttu-id="92dff-181">將 Azure 入口網站的 [指紋] 值貼至 [憑證指紋] 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="92dff-181">Paste the **Thumbprint** value from Azure portal into the **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="92dff-182">d.</span><span class="sxs-lookup"><span data-stu-id="92dff-182">d.</span></span> <span data-ttu-id="92dff-183">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="92dff-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="92dff-184">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="92dff-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="92dff-185">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="92dff-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="92dff-186">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="92dff-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="92dff-187">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="92dff-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="92dff-188">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="92dff-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="92dff-190">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="92dff-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="92dff-191">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="92dff-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="92dff-193">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="92dff-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="92dff-195">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="92dff-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="92dff-197">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="92dff-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="92dff-199">a.</span><span class="sxs-lookup"><span data-stu-id="92dff-199">a.</span></span> <span data-ttu-id="92dff-200">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="92dff-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="92dff-201">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="92dff-201">b.</span></span> <span data-ttu-id="92dff-202">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="92dff-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="92dff-203">c.</span><span class="sxs-lookup"><span data-stu-id="92dff-203">c.</span></span> <span data-ttu-id="92dff-204">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="92dff-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="92dff-205">d.</span><span class="sxs-lookup"><span data-stu-id="92dff-205">d.</span></span> <span data-ttu-id="92dff-206">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="92dff-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="92dff-207">建立 Bime 測試使用者</span><span class="sxs-lookup"><span data-stu-id="92dff-207">Creating a Bime test user</span></span>

<span data-ttu-id="92dff-208">若要讓 Azure AD 使用者可以登入 Bime，必須將他們佈建到 Bime。</span><span class="sxs-lookup"><span data-stu-id="92dff-208">In order to enable Azure AD users to log in to Bime, they must be provisioned into Bime.</span></span> <span data-ttu-id="92dff-209">Bime 需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="92dff-209">In the case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="92dff-210">**若要設定使用者佈建，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="92dff-210">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="92dff-211">登入您的 **Bime** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92dff-211">Log in to your **Bime** tenant.</span></span>

2. <span data-ttu-id="92dff-212">在工具列中，按一下 [管理]，然後按一下 [使用者]。</span><span class="sxs-lookup"><span data-stu-id="92dff-212">In the toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="92dff-213">![管理](./media/active-directory-saas-bime-tutorial/ic775561.png "管理")</span><span class="sxs-lookup"><span data-stu-id="92dff-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="92dff-214">在 [使用者清單] 中，按一下 新增使用者\("+")。</span><span class="sxs-lookup"><span data-stu-id="92dff-214">In the **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="92dff-215">![使用者](./media/active-directory-saas-bime-tutorial/ic775562.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="92dff-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="92dff-216">在 [使用者詳細資料]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="92dff-216">On the **User Details** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="92dff-217">![使用者詳細資料](./media/active-directory-saas-bime-tutorial/ic775563.png "使用者詳細資料")</span><span class="sxs-lookup"><span data-stu-id="92dff-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="92dff-218">a.</span><span class="sxs-lookup"><span data-stu-id="92dff-218">a.</span></span> <span data-ttu-id="92dff-219">在 [名字] 文字方塊中，輸入使用者的名字，例如 **Britta**。</span><span class="sxs-lookup"><span data-stu-id="92dff-219">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="92dff-220">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="92dff-220">b.</span></span> <span data-ttu-id="92dff-221">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 **Simon**。</span><span class="sxs-lookup"><span data-stu-id="92dff-221">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="92dff-222">c.</span><span class="sxs-lookup"><span data-stu-id="92dff-222">c.</span></span> <span data-ttu-id="92dff-223">在 [電子郵件] 文字方塊中，輸入使用者的電子郵件，例如 **brittasimon@contoso.com**。</span><span class="sxs-lookup"><span data-stu-id="92dff-223">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="92dff-224">d.</span><span class="sxs-lookup"><span data-stu-id="92dff-224">d.</span></span> <span data-ttu-id="92dff-225">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="92dff-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="92dff-226">您可以使用任何其他的 Bime 使用者帳戶建立工具或 Bime 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="92dff-226">You can use any other Bime user account creation tools or APIs provided by Bime to provision AAD user accounts.</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="92dff-227">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="92dff-227">Assigning the Azure AD test user</span></span>

<span data-ttu-id="92dff-228">在本節中，您會將 Bime 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="92dff-228">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Bime.</span></span>

![指派使用者][200] 

<span data-ttu-id="92dff-230">**若要將 Britta Simon 指派給 Bime，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="92dff-230">**To assign Britta Simon to Bime, perform the following steps:**</span></span>

1. <span data-ttu-id="92dff-231">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="92dff-231">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="92dff-233">在應用程式清單中，選取 [Bime] 。</span><span class="sxs-lookup"><span data-stu-id="92dff-233">In the applications list, select **Bime**.</span></span>

    ![設定單一登入](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="92dff-235">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="92dff-235">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="92dff-237">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92dff-237">Click **Add** button.</span></span> <span data-ttu-id="92dff-238">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="92dff-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="92dff-240">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="92dff-240">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="92dff-241">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92dff-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="92dff-242">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="92dff-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="92dff-243">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="92dff-243">Testing single sign-on</span></span>

<span data-ttu-id="92dff-244">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="92dff-244">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="92dff-245">當您在「存取面板」中按一下 [Bime] 圖格時，應該會自動登入您的 Bime 應用程式。</span><span class="sxs-lookup"><span data-stu-id="92dff-245">When you click the Bime tile in the Access Panel, you should get automatically signed-on to your Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="92dff-246">其他資源</span><span class="sxs-lookup"><span data-stu-id="92dff-246">Additional resources</span></span>

* [<span data-ttu-id="92dff-247">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="92dff-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="92dff-248">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="92dff-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

