---
title: "教學課程：Azure Active Directory 與 O.C.  Tanner - AppreciateHub 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 O.C. 之間的單一登入。 Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="f0f1a-105">教學課程：Azure Active Directory 與 O.C. </span><span class="sxs-lookup"><span data-stu-id="f0f1a-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="f0f1a-106">Tanner - AppreciateHub 的人員</span><span class="sxs-lookup"><span data-stu-id="f0f1a-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="f0f1a-107">在本教學課程中，您會了解如何將 O.C. </span><span class="sxs-lookup"><span data-stu-id="f0f1a-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="f0f1a-108">Tanner - AppreciateHub 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0f1a-109">整合 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-109">Integrating O.C.</span></span> <span data-ttu-id="f0f1a-110">Tanner - AppreciateHub 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0f1a-111">您可以在 Azure AD 中控制可存取 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="f0f1a-112">Tanner - AppreciateHub 的人員</span><span class="sxs-lookup"><span data-stu-id="f0f1a-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="f0f1a-113">您可以讓使用者使用其 Azure AD 帳戶自動登入到 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="f0f1a-114">Tanner - AppreciateHub (單一登入)</span><span class="sxs-lookup"><span data-stu-id="f0f1a-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0f1a-115">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="f0f1a-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0f1a-116">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0f1a-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0f1a-117">Prerequisites</span></span>

<span data-ttu-id="f0f1a-118">若要設定 Azure AD 與 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="f0f1a-119">Tanner - AppreciateHub 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="f0f1a-120">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f0f1a-120">An Azure AD subscription</span></span>
- <span data-ttu-id="f0f1a-121">啟用 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-121">A O.C.</span></span> <span data-ttu-id="f0f1a-122">Tanner - AppreciateHub 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="f0f1a-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0f1a-123">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0f1a-124">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0f1a-125">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0f1a-126">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0f1a-127">案例描述</span><span class="sxs-lookup"><span data-stu-id="f0f1a-127">Scenario description</span></span>
<span data-ttu-id="f0f1a-128">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0f1a-129">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0f1a-130">從組件庫新增 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-130">Adding O.C.</span></span> <span data-ttu-id="f0f1a-131">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="f0f1a-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="f0f1a-132">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f0f1a-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="f0f1a-133">從組件庫新增 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-133">Adding O.C.</span></span> <span data-ttu-id="f0f1a-134">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="f0f1a-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="f0f1a-135">若要設定將 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-135">To configure the integration of O.C.</span></span> <span data-ttu-id="f0f1a-136">Tanner - AppreciateHub 整合到 Azure AD，您需要從組件庫將 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="f0f1a-137">Tanner - AppreciateHub 新增至受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0f1a-138">**若要從組建庫新增 O.C.Tanner - AppreciateHub，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f0f1a-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0f1a-139">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0f1a-141">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0f1a-142">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-142">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="f0f1a-144">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="f0f1a-146">在搜尋方塊中，輸入 **O.C.Tanner - AppreciateHub**。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="f0f1a-148">在 [結果] 窗格中選取 **[O.C.Tanner - AppreciateHub]**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0f1a-150">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f0f1a-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0f1a-151">在本節中，您會設定及測試與 O.C. 搭配運作的 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f0f1a-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="f0f1a-152">Tanner - AppreciateHub。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0f1a-153">為使單一登入運作，Azure AD 必須知道 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="f0f1a-154">Tanner - AppreciateHub 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="f0f1a-155">換句話說，必須在 Azure AD 使用者和 O.C. </span><span class="sxs-lookup"><span data-stu-id="f0f1a-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="f0f1a-156">Tanner - AppreciateHub 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="f0f1a-157">在 O.C. </span><span class="sxs-lookup"><span data-stu-id="f0f1a-157">In O.C.</span></span> <span data-ttu-id="f0f1a-158">Tanner - AppreciateHub 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0f1a-159">若要設定和測試 Azure AD 單一登入與 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="f0f1a-160">Tanner - AppreciateHub，您必須完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0f1a-161">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0f1a-162">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f0f1a-163">**[建立 O.C.Tanner - AppreciateHub 測試使用者](#creating-a-oc-tanner---appreciatehub-test-user)** - 為了在 O.C. </span><span class="sxs-lookup"><span data-stu-id="f0f1a-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="f0f1a-164">Tanner - AppreciateHub 中有對應 Britta Simon 的使用者，以連結到 Azure AD 中代表的使用者。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f0f1a-165">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f0f1a-166">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0f1a-167">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="f0f1a-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0f1a-168">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 O.C. </span><span class="sxs-lookup"><span data-stu-id="f0f1a-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="f0f1a-169">Tanner - AppreciateHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="f0f1a-170">**若要設定 Azure AD 單一登入與 O.C.Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f0f1a-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="f0f1a-171">在 Azure 入口網站上**O.C.Tanner-AppreciateHub**應用程式整合頁面上，按一下 **單一登入**。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="f0f1a-173">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="f0f1a-175">在**O.C.Tanner-AppreciateHub 網域和 Url**區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="f0f1a-177">a.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-177">a.</span></span> <span data-ttu-id="f0f1a-178">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span><span class="sxs-lookup"><span data-stu-id="f0f1a-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0f1a-179">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-179">This value is not real.</span></span> <span data-ttu-id="f0f1a-180">請使用實際的「回覆 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="f0f1a-181">請連絡[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)取得此值。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="f0f1a-182">b.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-182">b.</span></span> <span data-ttu-id="f0f1a-183">使用下列連結開啟中繼資料檔案：[https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata)。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="f0f1a-184">c.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-184">c.</span></span> <span data-ttu-id="f0f1a-185">找出 [md:AssertionConsumerService] 節點。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="f0f1a-186">d.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-186">d.</span></span> <span data-ttu-id="f0f1a-187">複製 [位置] 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![設定 App 設定][12]
   
    <span data-ttu-id="f0f1a-189">e.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-189">e.</span></span> <span data-ttu-id="f0f1a-190">在[登入 URL] 文字方塊中，貼上您在上一個步驟中取得的值。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="f0f1a-191">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="f0f1a-193">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-193">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f0f1a-195">若要設定單一登入上**O.C.Tanner-AppreciateHub**端，您需要傳送下載**中繼資料 XML**至[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="f0f1a-196">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="f0f1a-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0f1a-197">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0f1a-198">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f0f1a-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0f1a-199">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f0f1a-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0f1a-200">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="f0f1a-202">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f0f1a-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0f1a-203">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0f1a-205">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0f1a-207">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0f1a-209">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f0f1a-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0f1a-211">a.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-211">a.</span></span> <span data-ttu-id="f0f1a-212">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0f1a-213">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-213">b.</span></span> <span data-ttu-id="f0f1a-214">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0f1a-215">c.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-215">c.</span></span> <span data-ttu-id="f0f1a-216">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0f1a-217">d.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-217">d.</span></span> <span data-ttu-id="f0f1a-218">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="f0f1a-219">建立 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-219">Creating a O.C.</span></span> <span data-ttu-id="f0f1a-220">Tanner - AppreciateHub 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f0f1a-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="f0f1a-221">本節目標是在 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="f0f1a-222">Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="f0f1a-223">**若要在 O.C.Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f0f1a-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="f0f1a-224">請要求您[O.C.Tanner-AppreciateHub 支援小組](mailto:sso@octanner.com)建立使用者，其具有與 nameID 屬性許 Simon 的使用者名稱相同的值在 Azure AD 中。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0f1a-225">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="f0f1a-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0f1a-226">在本節中，您會將 O.C. Tanner - AppreciateHub 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="f0f1a-227">Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-227">Tanner - AppreciateHub.</span></span>

![指派使用者][200] 

<span data-ttu-id="f0f1a-229">**若要將 Britta Simon 指派給 O.C.Tanner - AppreciateHub 中建立名為 Britta Simon 的使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="f0f1a-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="f0f1a-230">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="f0f1a-232">在應用程式清單中，選取 **O.C.Tanner - AppreciateHub**。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![設定單一登入](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="f0f1a-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="f0f1a-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-236">Click **Add** button.</span></span> <span data-ttu-id="f0f1a-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="f0f1a-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0f1a-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0f1a-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0f1a-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="f0f1a-242">Testing single sign-on</span></span>

<span data-ttu-id="f0f1a-243">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f0f1a-244">當您在 存取面板 按一下 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-244">When you click the O.C.</span></span> <span data-ttu-id="f0f1a-245">Tanner - AppreciateHub 磚時，應該會自動登入您的 O.C.</span><span class="sxs-lookup"><span data-stu-id="f0f1a-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="f0f1a-246">Tanner - AppreciateHub 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f0f1a-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0f1a-247">其他資源</span><span class="sxs-lookup"><span data-stu-id="f0f1a-247">Additional resources</span></span>

* [<span data-ttu-id="f0f1a-248">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="f0f1a-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0f1a-249">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="f0f1a-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

