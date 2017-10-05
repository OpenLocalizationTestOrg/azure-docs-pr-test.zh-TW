---
title: "教學課程：Azure Active Directory 與 TOPdesk - Public 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TOPdesk - Public 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: f21fe0b363776974108ff460060e4c15a51a58a3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a><span data-ttu-id="4b434-103">教學課程：Azure Active Directory 與 TOPdesk - Public 整合</span><span class="sxs-lookup"><span data-stu-id="4b434-103">Tutorial: Azure Active Directory integration with TOPdesk - Public</span></span>

<span data-ttu-id="4b434-104">在本教學課程中，您將了解如何整合 TOPdesk - Public 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4b434-104">In this tutorial, you learn how to integrate TOPdesk - Public with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4b434-105">TOPdesk - Public 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4b434-105">Integrating TOPdesk - Public with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4b434-106">您可以在 Azure AD 中控制可存取 TOPdesk - Public 的人員。</span><span class="sxs-lookup"><span data-stu-id="4b434-106">You can control in Azure AD who has access to TOPdesk - Public.</span></span>
- <span data-ttu-id="4b434-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TOPdesk - Public (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="4b434-107">You can enable your users to automatically get signed-on to TOPdesk - Public (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4b434-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b434-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4b434-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4b434-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b434-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4b434-110">Prerequisites</span></span>

<span data-ttu-id="4b434-111">若要設定 Azure AD 與 TOPdesk - Public 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4b434-111">To configure Azure AD integration with TOPdesk - Public, you need the following items:</span></span>

- <span data-ttu-id="4b434-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b434-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4b434-113">已啟用 TOPdesk - Public 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4b434-113">A TOPdesk - Public single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4b434-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4b434-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4b434-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4b434-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4b434-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4b434-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4b434-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4b434-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4b434-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4b434-118">Scenario description</span></span>
<span data-ttu-id="4b434-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4b434-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4b434-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4b434-121">從資源庫新增 TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="4b434-121">Adding TOPdesk - Public from the gallery</span></span>
2. <span data-ttu-id="4b434-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b434-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---public-from-the-gallery"></a><span data-ttu-id="4b434-123">從資源庫新增 TOPdesk - Public</span><span class="sxs-lookup"><span data-stu-id="4b434-123">Adding TOPdesk - Public from the gallery</span></span>
<span data-ttu-id="4b434-124">若要設定將TOPdesk - Public 整合到 Azure AD 中，您需要從資源庫將 TOPdesk - Public 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="4b434-124">To configure the integration of TOPdesk - Public into Azure AD, you need to add TOPdesk - Public from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4b434-125">**若要從資源庫新增 TOPdesk - Public，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b434-125">**To add TOPdesk - Public from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4b434-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4b434-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="4b434-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b434-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4b434-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b434-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="4b434-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b434-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="4b434-133">在搜尋方塊中，輸入 **TOPdesk - Public**，從結果面板中選取 [TOPdesk - Public]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b434-133">In the search box, type **TOPdesk - Public**, select **TOPdesk - Public** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4b434-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b434-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4b434-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 TOPdesk - Public 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Public based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4b434-137">若要讓單一登入運作，Azure AD 必須知道 TOPdesk - Public 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4b434-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Public is to a user in Azure AD.</span></span> <span data-ttu-id="4b434-138">換句話說，必須在 Azure AD 使用者和 TOPdesk - Public 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4b434-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Public needs to be established.</span></span>

<span data-ttu-id="4b434-139">在 TOPdesk - Public 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4b434-139">In TOPdesk - Public, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4b434-140">若要設定及測試與 TOPdesk - Public 搭配運作的 Azure AD 單一登入，您需要完成下列建構元素：</span><span class="sxs-lookup"><span data-stu-id="4b434-140">To configure and test Azure AD single sign-on with TOPdesk - Public, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4b434-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4b434-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4b434-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4b434-143">**[建立 TOPdesk - Public 測試使用者](#create-a-topdesk---public-test-user)** - 使 TOPdesk - Public 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="4b434-143">**[Create a TOPdesk - Public test user](#create-a-topdesk---public-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Public that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4b434-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4b434-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="4b434-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4b434-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4b434-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4b434-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TOPdesk - Public 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Public application.</span></span>

<span data-ttu-id="4b434-148">**若要使用 TOPdesk - Publice 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b434-148">**To configure Azure AD single sign-on with TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="4b434-149">在 Azure 入口網站的 [TOPdesk - Public] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4b434-149">In the Azure portal, on the **TOPdesk - Public** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="4b434-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. <span data-ttu-id="4b434-153">在 [TOPdesk - Public 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-153">On the **TOPdesk - Public Domain and URLs** section, perform the following steps:</span></span>

    ![TOPdesk - Public 網域與 URL 單一登入資訊](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    <span data-ttu-id="4b434-155">a.</span><span class="sxs-lookup"><span data-stu-id="4b434-155">a.</span></span> <span data-ttu-id="4b434-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="4b434-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>
    
    <span data-ttu-id="4b434-157">b.</span><span class="sxs-lookup"><span data-stu-id="4b434-157">b.</span></span> <span data-ttu-id="4b434-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.topdesk.net/tas/public/login/verify`</span><span class="sxs-lookup"><span data-stu-id="4b434-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/verify`</span></span>

    <span data-ttu-id="4b434-159">c.</span><span class="sxs-lookup"><span data-stu-id="4b434-159">c.</span></span> <span data-ttu-id="4b434-160">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="4b434-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="4b434-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4b434-161">These values are not real.</span></span> <span data-ttu-id="4b434-162">使用實際的識別碼、回覆 URL 和登入 URL 來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="4b434-162">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="4b434-163">[回覆 URL] 稍後會在本教學課程中說明。</span><span class="sxs-lookup"><span data-stu-id="4b434-163">Reply URL is explaned later in tutorial.</span></span> <span data-ttu-id="4b434-164">請連絡 [TOPdesk - Public 用戶端支援小組](https://help.topdesk.com/saas/enterprise/user/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="4b434-164">Contact [TOPdesk - Public Client support team](https://help.topdesk.com/saas/enterprise/user/) to get these values.</span></span>  

4. <span data-ttu-id="4b434-165">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4b434-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. <span data-ttu-id="4b434-167">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b434-167">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="4b434-169">在 [TOPdesk - Public 設定] 區段中，按一下 [設定 TOPdesk - Public] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4b434-169">On the **TOPdesk - Public Configuration** section, click **Configure TOPdesk - Public** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4b434-170">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4b434-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TOPdesk - Public 設定](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. <span data-ttu-id="4b434-172">以系統管理員身分登入您的 **TOPdesk - Public** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4b434-172">Sign on to your **TOPdesk - Public** company site as an administrator.</span></span>

8. <span data-ttu-id="4b434-173">在 [TOPdesk] 功能表中按一下 [設定]。</span><span class="sxs-lookup"><span data-stu-id="4b434-173">In the **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="4b434-174">![設定](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "設定")</span><span class="sxs-lookup"><span data-stu-id="4b434-174">![Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="4b434-175">按一下 [登入設定] 。</span><span class="sxs-lookup"><span data-stu-id="4b434-175">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="4b434-176">![登入設定](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "登入設定")</span><span class="sxs-lookup"><span data-stu-id="4b434-176">![Login Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="4b434-177">展開 [登入設定] 功能表，然後按一下 [一般]。</span><span class="sxs-lookup"><span data-stu-id="4b434-177">Expand the **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="4b434-178">![一般](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "一般")</span><span class="sxs-lookup"><span data-stu-id="4b434-178">![General](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="4b434-179">在 [SAML 登入] 組態區段的 [Public] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-179">In the **Public** section of the **SAML login** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="4b434-180">![技術設定](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "技術設定")</span><span class="sxs-lookup"><span data-stu-id="4b434-180">![Technical Settings](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Technical Settings")</span></span>
   
    <span data-ttu-id="4b434-181">a.</span><span class="sxs-lookup"><span data-stu-id="4b434-181">a.</span></span> <span data-ttu-id="4b434-182">按 [下載]  來下載公用中繼資料檔案，然後再將它儲存在本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="4b434-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="4b434-183">b.</span><span class="sxs-lookup"><span data-stu-id="4b434-183">b.</span></span> <span data-ttu-id="4b434-184">開啟下載的中繼資料檔案，然後找到 **AssertionConsumerService** 節點。</span><span class="sxs-lookup"><span data-stu-id="4b434-184">Open the downloaded metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="4b434-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span><span class="sxs-lookup"><span data-stu-id="4b434-185">![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")</span></span>
   
    <span data-ttu-id="4b434-186">c.</span><span class="sxs-lookup"><span data-stu-id="4b434-186">c.</span></span> <span data-ttu-id="4b434-187">複製 **AssertionConsumerService** 值，在 [TOPdesk - Public 網域與 URL] 區段的 [回覆 URL] 文字方塊中，貼上此值。</span><span class="sxs-lookup"><span data-stu-id="4b434-187">Copy the **AssertionConsumerService** value, paste this value in the **Reply URL** textbox in **TOPdesk - Public Domain and URLs** section.</span></span>      
   
12. <span data-ttu-id="4b434-188">若要建立憑證檔案，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-188">To create a certificate file, perform the following steps:</span></span>
    
    <span data-ttu-id="4b434-189">![憑證](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "憑證")</span><span class="sxs-lookup"><span data-stu-id="4b434-189">![Certificate](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificate")</span></span>
    
    <span data-ttu-id="4b434-190">a.</span><span class="sxs-lookup"><span data-stu-id="4b434-190">a.</span></span> <span data-ttu-id="4b434-191">從 Azure 入口網站開啟下載的中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="4b434-191">Open the downloaded metadata file from Azure portal.</span></span>
    
    <span data-ttu-id="4b434-192">b.</span><span class="sxs-lookup"><span data-stu-id="4b434-192">b.</span></span> <span data-ttu-id="4b434-193">展開 **RoleDescriptor** 節點，其具有 **fed:ApplicationServiceType** 的 **xsi:type**。</span><span class="sxs-lookup"><span data-stu-id="4b434-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    
    <span data-ttu-id="4b434-194">c.</span><span class="sxs-lookup"><span data-stu-id="4b434-194">c.</span></span> <span data-ttu-id="4b434-195">複製 **X509Certificate** 節點的值。</span><span class="sxs-lookup"><span data-stu-id="4b434-195">Copy the value of the **X509Certificate** node.</span></span>
    
    <span data-ttu-id="4b434-196">d.</span><span class="sxs-lookup"><span data-stu-id="4b434-196">d.</span></span> <span data-ttu-id="4b434-197">儲存複製的 **X509Certificate** 值到本機電腦的檔案中。</span><span class="sxs-lookup"><span data-stu-id="4b434-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="4b434-198">在 **Public** 區段中，按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="4b434-198">In the **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="4b434-199">![SAML 登入](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML 登入")</span><span class="sxs-lookup"><span data-stu-id="4b434-199">![SAML Login](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "SAML Login")</span></span>

14. <span data-ttu-id="4b434-200">在 [SAML 組態輔助程式]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>
    
    <span data-ttu-id="4b434-201">![SAML 組態輔助程式](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML 組態輔助程式")</span><span class="sxs-lookup"><span data-stu-id="4b434-201">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="4b434-202">a.</span><span class="sxs-lookup"><span data-stu-id="4b434-202">a.</span></span> <span data-ttu-id="4b434-203">若要上傳您從 Azure 入口網站下載的中繼資料檔案，請在 [同盟中繼資料] 下按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="4b434-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="4b434-204">b.</span><span class="sxs-lookup"><span data-stu-id="4b434-204">b.</span></span> <span data-ttu-id="4b434-205">若要上傳您的憑證檔案，請在 [憑證 (RSA)] 下按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="4b434-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="4b434-206">c.</span><span class="sxs-lookup"><span data-stu-id="4b434-206">c.</span></span> <span data-ttu-id="4b434-207">若要上傳您從 TOPdesk 支援小組取得的標誌檔案，請在 [標誌圖示] 下按一下 [瀏覽]。</span><span class="sxs-lookup"><span data-stu-id="4b434-207">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="4b434-208">d.</span><span class="sxs-lookup"><span data-stu-id="4b434-208">d.</span></span> <span data-ttu-id="4b434-209">在 [使用者名稱屬性] 文字方塊中，輸入 `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`。</span><span class="sxs-lookup"><span data-stu-id="4b434-209">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="4b434-210">e.</span><span class="sxs-lookup"><span data-stu-id="4b434-210">e.</span></span> <span data-ttu-id="4b434-211">在 [顯示名稱]  文字方塊中，輸入您的組態名稱。</span><span class="sxs-lookup"><span data-stu-id="4b434-211">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="4b434-212">f.</span><span class="sxs-lookup"><span data-stu-id="4b434-212">f.</span></span> <span data-ttu-id="4b434-213">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4b434-213">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="4b434-214">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="4b434-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4b434-215">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4b434-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4b434-216">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4b434-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4b434-217">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b434-217">Create an Azure AD test user</span></span>

<span data-ttu-id="4b434-218">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4b434-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="4b434-220">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b434-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4b434-221">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b434-221">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4b434-223">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4b434-223">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4b434-225">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4b434-225">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4b434-227">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-227">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4b434-229">a.</span><span class="sxs-lookup"><span data-stu-id="4b434-229">a.</span></span> <span data-ttu-id="4b434-230">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4b434-230">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4b434-231">b.</span><span class="sxs-lookup"><span data-stu-id="4b434-231">b.</span></span> <span data-ttu-id="4b434-232">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="4b434-232">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4b434-233">c.</span><span class="sxs-lookup"><span data-stu-id="4b434-233">c.</span></span> <span data-ttu-id="4b434-234">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="4b434-234">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4b434-235">d.</span><span class="sxs-lookup"><span data-stu-id="4b434-235">d.</span></span> <span data-ttu-id="4b434-236">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4b434-236">Click **Create**.</span></span>
 
### <a name="create-a-topdesk---public-test-user"></a><span data-ttu-id="4b434-237">建立 TOPdesk-Public 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b434-237">Create a TOPdesk - Public test user</span></span>

<span data-ttu-id="4b434-238">若要讓 Azure AD 使用者可以登入 TOPdesk - Public，則必須將他們佈建到 TOPdesk - Public。</span><span class="sxs-lookup"><span data-stu-id="4b434-238">In order to enable Azure AD users to log into TOPdesk - Public, they must be provisioned into TOPdesk - Public.</span></span>  
<span data-ttu-id="4b434-239">TOPdesk - Public 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="4b434-239">In the case of TOPdesk - Public, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="4b434-240">若要設定使用者佈建，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-240">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="4b434-241">以系統管理員身分登入您的 **TOPdesk - Public** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="4b434-241">Sign on to your **TOPdesk - Public** company site as administrator.</span></span>

2. <span data-ttu-id="4b434-242">在上方功能表中按一下 [TOPdesk] \> [新增] \> [支援檔案] \> [人員]。</span><span class="sxs-lookup"><span data-stu-id="4b434-242">In the menu on the top, click **TOPdesk \> New \> Support Files \> Person**.</span></span>
   
    <span data-ttu-id="4b434-243">![人員](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "人員")</span><span class="sxs-lookup"><span data-stu-id="4b434-243">![Person](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Person")</span></span>

3. <span data-ttu-id="4b434-244">在 [新增人員] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4b434-244">On the New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="4b434-245">![新增人員](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "新增人員")</span><span class="sxs-lookup"><span data-stu-id="4b434-245">![New Person](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "New Person")</span></span>
   
    <span data-ttu-id="4b434-246">a.</span><span class="sxs-lookup"><span data-stu-id="4b434-246">a.</span></span> <span data-ttu-id="4b434-247">按一下 [一般] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4b434-247">Click the General tab.</span></span>

    <span data-ttu-id="4b434-248">b.</span><span class="sxs-lookup"><span data-stu-id="4b434-248">b.</span></span> <span data-ttu-id="4b434-249">在 [姓氏] 文字方塊中，輸入使用者的姓氏，例如 Simon</span><span class="sxs-lookup"><span data-stu-id="4b434-249">In the **Surname** textbox, type Surname of the user like Simon</span></span>
 
    <span data-ttu-id="4b434-250">c.</span><span class="sxs-lookup"><span data-stu-id="4b434-250">c.</span></span> <span data-ttu-id="4b434-251">選取該帳戶的 **網站** 。</span><span class="sxs-lookup"><span data-stu-id="4b434-251">Select a **Site** for the account.</span></span>
 
    <span data-ttu-id="4b434-252">d.</span><span class="sxs-lookup"><span data-stu-id="4b434-252">d.</span></span> <span data-ttu-id="4b434-253">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="4b434-253">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="4b434-254">您可以使用任何其他的 TOPdesk - Public 使用者帳戶建立工具或 TOPdesk - Public 提供的 API 來佈建 Azure AD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="4b434-254">You can use any other TOPdesk - Public user account creation tools or APIs provided by TOPdesk - Public to provision Azure AD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4b434-255">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4b434-255">Assign the Azure AD test user</span></span>

<span data-ttu-id="4b434-256">在本節中，您會將 TOPdesk - Public 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4b434-256">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Public.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="4b434-258">**若要指派 Britta Simon 給 TOPdesk - Public，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4b434-258">**To assign Britta Simon to TOPdesk - Public, perform the following steps:**</span></span>

1. <span data-ttu-id="4b434-259">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4b434-259">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4b434-261">在應用程式清單中，選取 [TOPdesk-Public]。</span><span class="sxs-lookup"><span data-stu-id="4b434-261">In the applications list, select **TOPdesk - Public**.</span></span>

    ![應用程式清單中的 TOPdesk - Public 連結](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. <span data-ttu-id="4b434-263">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b434-263">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="4b434-265">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b434-265">Click **Add** button.</span></span> <span data-ttu-id="4b434-266">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4b434-266">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="4b434-268">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4b434-268">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4b434-269">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b434-269">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4b434-270">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4b434-270">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4b434-271">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4b434-271">Test single sign-on</span></span>

<span data-ttu-id="4b434-272">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="4b434-272">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="4b434-273">當您在存取面板中按一下 [TOPdesk - Public] 圖格時，應該會自動登入您的 TOPdesk - Public 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b434-273">When you click the TOPdesk - Public tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Public application.</span></span>
<span data-ttu-id="4b434-274">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="4b434-274">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4b434-275">其他資源</span><span class="sxs-lookup"><span data-stu-id="4b434-275">Additional resources</span></span>

* [<span data-ttu-id="4b434-276">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4b434-276">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4b434-277">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4b434-277">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

