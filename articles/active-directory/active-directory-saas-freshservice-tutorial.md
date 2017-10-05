---
title: "教學課程：Azure Active Directory 與 Freshservice 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Freshservice 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="1e5c3-103">教學課程：Azure Active Directory 與 Freshservice 整合</span><span class="sxs-lookup"><span data-stu-id="1e5c3-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="1e5c3-104">在本教學課程中，您將了解如何整合 Freshservice 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1e5c3-105">Freshservice 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1e5c3-106">您可以在 Azure AD 中控制可存取 Freshservice 的人員</span><span class="sxs-lookup"><span data-stu-id="1e5c3-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="1e5c3-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Freshservice (單一登入)</span><span class="sxs-lookup"><span data-stu-id="1e5c3-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1e5c3-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="1e5c3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1e5c3-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e5c3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1e5c3-110">Prerequisites</span></span>

<span data-ttu-id="1e5c3-111">若要設定 Azure AD 與 Freshservice 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="1e5c3-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1e5c3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1e5c3-113">已啟用 Freshservice 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1e5c3-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1e5c3-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1e5c3-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1e5c3-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1e5c3-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1e5c3-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="1e5c3-118">Scenario description</span></span>
<span data-ttu-id="1e5c3-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1e5c3-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1e5c3-121">從資源庫新增 Freshservice</span><span class="sxs-lookup"><span data-stu-id="1e5c3-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="1e5c3-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1e5c3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="1e5c3-123">從資源庫新增 Freshservice</span><span class="sxs-lookup"><span data-stu-id="1e5c3-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="1e5c3-124">若要設定將 Freshservice 整合到 Azure AD 中，您需要從資源庫將 Freshservice 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1e5c3-125">**若要從資源庫新增 Freshservice，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1e5c3-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5c3-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1e5c3-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1e5c3-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="1e5c3-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="1e5c3-133">在搜尋方塊中，輸入 **Freshservice**。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-133">In the search box, type **Freshservice**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="1e5c3-135">在結果窗格中，選取 [Freshservice]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1e5c3-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1e5c3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1e5c3-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Freshservice 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1e5c3-139">若要讓單一登入運作，Azure AD 必須知道 Freshservice 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="1e5c3-140">換句話說，必須在 Azure AD 使用者和 Freshservice 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="1e5c3-141">在 Freshservice 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1e5c3-142">若要設定及測試與 Freshservice 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1e5c3-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1e5c3-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1e5c3-145">**[建立 Freshservice 測試使用者](#creating-a-freshservice-test-user)** - 在 Freshservice 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1e5c3-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1e5c3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1e5c3-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="1e5c3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1e5c3-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Freshservice 中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="1e5c3-150">**若要使用 Freshservice 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1e5c3-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5c3-151">在 Azure 入口網站的 [Freshservice] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="1e5c3-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="1e5c3-155">在 [Freshservice 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="1e5c3-157">a.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-157">a.</span></span> <span data-ttu-id="1e5c3-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="1e5c3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="1e5c3-159">b.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-159">b.</span></span> <span data-ttu-id="1e5c3-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="1e5c3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1e5c3-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-161">These values are not real.</span></span> <span data-ttu-id="1e5c3-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1e5c3-163">請連絡 [Freshservice 用戶端支援小組](https://support.freshservice.com/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="1e5c3-164">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="1e5c3-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1e5c3-168">在 [Freshservice 組態] 區段上，按一下 [設定 Freshservice] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="1e5c3-169">從 [快速參考] 區段中複製 [登出 URL 和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="1e5c3-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Freshservice 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="1e5c3-172">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="1e5c3-173">![管理](./media/active-directory-saas-freshservice-tutorial/ic790814.png "管理")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="1e5c3-174">在 [客戶入口網站] 中，按一下 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="1e5c3-175">![安全性](./media/active-directory-saas-freshservice-tutorial/ic790815.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="1e5c3-176">在 [安全性]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1e5c3-177">![單一登入](./media/active-directory-saas-freshservice-tutorial/ic790816.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="1e5c3-178">a.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-178">a.</span></span> <span data-ttu-id="1e5c3-179">將 [單一登入] 切換為 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="1e5c3-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-180">b.</span></span> <span data-ttu-id="1e5c3-181">選取 [SAML SSO] 。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="1e5c3-182">c.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-182">c.</span></span> <span data-ttu-id="1e5c3-183">在 [SAML 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的**「SAML 單一登入服務 URL」**值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1e5c3-184">d.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-184">d.</span></span> <span data-ttu-id="1e5c3-185">在 [登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1e5c3-186">e.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-186">e.</span></span> <span data-ttu-id="1e5c3-187">在 [安全性憑證指紋] 文字方塊中，貼上您從 Azure 入口網站複製的憑證 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="1e5c3-188">f.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-188">f.</span></span> <span data-ttu-id="1e5c3-189">按一下 [儲存] </span><span class="sxs-lookup"><span data-stu-id="1e5c3-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="1e5c3-190">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="1e5c3-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1e5c3-191">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1e5c3-192">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1e5c3-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1e5c3-193">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1e5c3-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="1e5c3-194">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="1e5c3-196">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1e5c3-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5c3-197">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1e5c3-199">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1e5c3-201">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1e5c3-203">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1e5c3-205">a.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-205">a.</span></span> <span data-ttu-id="1e5c3-206">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1e5c3-207">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-207">b.</span></span> <span data-ttu-id="1e5c3-208">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1e5c3-209">c.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-209">c.</span></span> <span data-ttu-id="1e5c3-210">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1e5c3-211">d.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-211">d.</span></span> <span data-ttu-id="1e5c3-212">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="1e5c3-213">建立 Freshservice 測試使用者</span><span class="sxs-lookup"><span data-stu-id="1e5c3-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="1e5c3-214">若要讓 Azure AD 使用者可以登入 FreshService，必須將他們佈建到 FreshService。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="1e5c3-215">FreshService 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="1e5c3-216">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1e5c3-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5c3-217">以系統管理員身分登入您的 **FreshService** 公司網站。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="1e5c3-218">在頂端的功能表中，按一下 [系統管理員] 。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="1e5c3-219">![管理](./media/active-directory-saas-freshservice-tutorial/ic790814.png "管理")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="1e5c3-220">在 [使用者管理] 區段中，按一下 [要求者]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="1e5c3-221">![要求者](./media/active-directory-saas-freshservice-tutorial/ic790818.png "要求者")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="1e5c3-222">按一下 [新要求者] 。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="1e5c3-223">![新要求者](./media/active-directory-saas-freshservice-tutorial/ic790819.png "新要求者")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="1e5c3-224">在 [新要求者]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="1e5c3-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="1e5c3-225">![新要求者](./media/active-directory-saas-freshservice-tutorial/ic790820.png "新要求者")</span><span class="sxs-lookup"><span data-stu-id="1e5c3-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="1e5c3-226">a.</span><span class="sxs-lookup"><span data-stu-id="1e5c3-226">a.</span></span> <span data-ttu-id="1e5c3-227">在相關的文字方塊中，輸入您要佈建之有效 Azure Active Directory 帳戶的**名字**和**電子郵件**屬性。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="1e5c3-228">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-228">b.</span></span> <span data-ttu-id="1e5c3-229">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="1e5c3-230">Azure Active Directory 帳戶的持有者會收到一封包含連結的電子郵件，以在啟用帳戶前進行確認</span><span class="sxs-lookup"><span data-stu-id="1e5c3-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="1e5c3-231">您可以使用任何其他的 FreshService 使用者帳戶建立工具或 FreshService 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![指派使用者][200] 

<span data-ttu-id="1e5c3-233">**若要將 Britta Simon 指派給 Freshservice，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="1e5c3-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="1e5c3-234">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="1e5c3-236">在應用程式清單中，選取 [Freshservice]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-236">In the applications list, select **Freshservice**.</span></span>

    ![設定單一登入](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="1e5c3-238">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-238">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="1e5c3-240">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-240">Click **Add** button.</span></span> <span data-ttu-id="1e5c3-241">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="1e5c3-243">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1e5c3-244">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1e5c3-245">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1e5c3-246">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="1e5c3-246">Testing single sign-on</span></span>

<span data-ttu-id="1e5c3-247">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1e5c3-248">當您在存取面板中按一下 [Freshservice] 圖格時，應該會自動登入 [Freshservice] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e5c3-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1e5c3-249">其他資源</span><span class="sxs-lookup"><span data-stu-id="1e5c3-249">Additional resources</span></span>

* [<span data-ttu-id="1e5c3-250">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="1e5c3-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1e5c3-251">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="1e5c3-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

