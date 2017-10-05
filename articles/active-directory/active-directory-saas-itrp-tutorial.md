---
title: "教學課程：Azure Active Directory 與 ITRP 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ITRP 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: fae1c7b6b0e04c1e23123d3aee7913cb3131e645
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="d616c-103">教學課程：Azure Active Directory 與 ITRP 整合</span><span class="sxs-lookup"><span data-stu-id="d616c-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="d616c-104">在本教學課程中，您會了解如何整合 ITRP 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d616c-104">In this tutorial, you learn how to integrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d616c-105">ITRP 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d616c-105">Integrating ITRP with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d616c-106">您可以在 Azure AD 中控制可存取 ITRP 的人員</span><span class="sxs-lookup"><span data-stu-id="d616c-106">You can control in Azure AD who has access to ITRP</span></span>
- <span data-ttu-id="d616c-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ITRP (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d616c-107">You can enable your users to automatically get signed-on to ITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d616c-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d616c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d616c-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d616c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d616c-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d616c-110">Prerequisites</span></span>

<span data-ttu-id="d616c-111">若要設定 Azure AD 與 ITRP 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d616c-111">To configure Azure AD integration with ITRP, you need the following items:</span></span>

- <span data-ttu-id="d616c-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d616c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d616c-113">已啟用 ITRP 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d616c-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d616c-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d616c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d616c-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d616c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d616c-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d616c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d616c-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d616c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d616c-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d616c-118">Scenario description</span></span>
<span data-ttu-id="d616c-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d616c-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d616c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d616c-121">從資源庫新增 ITRP</span><span class="sxs-lookup"><span data-stu-id="d616c-121">Adding ITRP from the gallery</span></span>
2. <span data-ttu-id="d616c-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d616c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-the-gallery"></a><span data-ttu-id="d616c-123">從資源庫新增 ITRP</span><span class="sxs-lookup"><span data-stu-id="d616c-123">Adding ITRP from the gallery</span></span>
<span data-ttu-id="d616c-124">若要設定將 ITRP 整合到 Azure AD 中，您需要從資源庫將 ITRP 新增到受管理的 SaaS app 清單。</span><span class="sxs-lookup"><span data-stu-id="d616c-124">To configure the integration of ITRP in to Azure AD, you need to add ITRP from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d616c-125">**若要從資源庫新增 ITRP，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d616c-125">**To add ITRP from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d616c-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d616c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d616c-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d616c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d616c-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d616c-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d616c-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d616c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d616c-133">在搜尋方塊中，輸入 **ITRP**。</span><span class="sxs-lookup"><span data-stu-id="d616c-133">In the search box, type **ITRP**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="d616c-135">在結果窗格中，選取 [ITRP]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d616c-135">In the results panel, select **ITRP**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d616c-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d616c-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="d616c-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 ITRP 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d616c-139">若要讓單一登入運作，Azure AD 必須知道 ITRP 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d616c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ITRP is to a user in Azure AD.</span></span> <span data-ttu-id="d616c-140">換句話說，必須建立 Azure AD 使用者和 ITRP 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d616c-140">In other words, a link relationship between an Azure AD user and the related user in ITRP needs to be established.</span></span>

<span data-ttu-id="d616c-141">在 ITRP 中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d616c-141">In ITRP, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d616c-142">若要設定及測試與 ITRP 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="d616c-142">To configure and test Azure AD single sign-on with ITRP, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d616c-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d616c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d616c-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d616c-145">**[建立 ITRP 測試使用者](#creating-an-itrp-test-user)** - 使 ITRP 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="d616c-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - to have a counterpart of Britta Simon in ITRP that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d616c-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d616c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d616c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d616c-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d616c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d616c-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ITRP 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="d616c-150">**若要設定與 ITRP 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d616c-150">**To configure Azure AD single sign-on with ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="d616c-151">在 Azure 入口網站的 [ITRP] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d616c-151">In the Azure portal, on the **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d616c-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="d616c-155">在 [ITRP 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d616c-155">On the **ITRP Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="d616c-157">a.</span><span class="sxs-lookup"><span data-stu-id="d616c-157">a.</span></span> <span data-ttu-id="d616c-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="d616c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="d616c-159">b.</span><span class="sxs-lookup"><span data-stu-id="d616c-159">b.</span></span> <span data-ttu-id="d616c-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="d616c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d616c-161">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d616c-161">These values are not real.</span></span> <span data-ttu-id="d616c-162">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d616c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d616c-163">請連絡 [ITRP 用戶端支援小組](https://www.itrp.com/support)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="d616c-163">Contact [ITRP Client support team](https://www.itrp.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="d616c-164">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="d616c-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="d616c-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d616c-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d616c-168">在 [ITRP 組態] 區段上，按一下 [設定 ITRP] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d616c-168">On the **ITRP Configuration** section, click **Configure ITRP** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d616c-169">從 [快速參考]區段中複製 [SAML 單一登入服務 URL 和登出 URL]。</span><span class="sxs-lookup"><span data-stu-id="d616c-169">Copy the **SAML Single Sign-On Service URL and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="d616c-171">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ITRP 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d616c-171">In a different web browser window, log in to your ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="d616c-172">在頂端的工具列中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-172">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="d616c-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="d616c-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="d616c-174">在左導覽窗格中，選取 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-174">In the left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="d616c-175">![單一登入](./media/active-directory-saas-itrp-tutorial/ic775571.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="d616c-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="d616c-176">在 [單一登入] 設定頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d616c-176">In the Single Sign-On configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="d616c-177">![單一登入](./media/active-directory-saas-itrp-tutorial/ic775572.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="d616c-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="d616c-178">![單一登入](./media/active-directory-saas-itrp-tutorial/ic775573.png "單一登入")</span><span class="sxs-lookup"><span data-stu-id="d616c-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="d616c-179">a.</span><span class="sxs-lookup"><span data-stu-id="d616c-179">a.</span></span> <span data-ttu-id="d616c-180">按一下 [啟用] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-180">Click **Enable**.</span></span>

    <span data-ttu-id="d616c-181">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d616c-181">b.</span></span> <span data-ttu-id="d616c-182">在 [遠端登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d616c-182">In **Remote Log Out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d616c-183">c.</span><span class="sxs-lookup"><span data-stu-id="d616c-183">c.</span></span> <span data-ttu-id="d616c-184">在 [SAML SSO URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d616c-184">In **SAML SSO URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d616c-185">d. 在 [憑證指紋] 文字方塊中，貼上您從 Azure 入口網站複製的憑證 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="d616c-185">d.In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="d616c-186">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d616c-187">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d616c-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d616c-188">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d616c-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d616c-189">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d616c-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d616c-190">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d616c-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="d616c-191">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d616c-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d616c-193">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d616c-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d616c-194">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d616c-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d616c-196">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d616c-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d616c-198">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d616c-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d616c-200">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d616c-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d616c-202">a.</span><span class="sxs-lookup"><span data-stu-id="d616c-202">a.</span></span> <span data-ttu-id="d616c-203">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d616c-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d616c-204">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d616c-204">b.</span></span> <span data-ttu-id="d616c-205">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d616c-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d616c-206">c.</span><span class="sxs-lookup"><span data-stu-id="d616c-206">c.</span></span> <span data-ttu-id="d616c-207">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d616c-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d616c-208">d.</span><span class="sxs-lookup"><span data-stu-id="d616c-208">d.</span></span> <span data-ttu-id="d616c-209">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="d616c-210">建立 ITRP 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d616c-210">Creating an ITRP test user</span></span>

<span data-ttu-id="d616c-211">若要讓 Azure AD 使用者可以登入 ITRP，必須將他們佈建到 ITRP。</span><span class="sxs-lookup"><span data-stu-id="d616c-211">To enable Azure AD users to log in to ITRP, they must be provisioned in to ITRP.</span></span>  

<span data-ttu-id="d616c-212">在 ITRP 的情況下，佈建是手動工作。</span><span class="sxs-lookup"><span data-stu-id="d616c-212">In the case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="d616c-213">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d616c-213">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d616c-214">登入您的 **ITRP** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="d616c-214">Log in to your **ITRP** tenant.</span></span>

2. <span data-ttu-id="d616c-215">在頂端的工具列中，按一下 [記錄] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-215">In the toolbar on the top, click **Records**.</span></span>
   
    <span data-ttu-id="d616c-216">![管理](./media/active-directory-saas-itrp-tutorial/ic775575.png "管理")</span><span class="sxs-lookup"><span data-stu-id="d616c-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="d616c-217">選取快顯功能表中的 [人員] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-217">From the popup menu, select **People**.</span></span>
   
    <span data-ttu-id="d616c-218">![人員](./media/active-directory-saas-itrp-tutorial/ic775587.png "人員")</span><span class="sxs-lookup"><span data-stu-id="d616c-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="d616c-219">按一下 [新增人員]  \(“+”)。</span><span class="sxs-lookup"><span data-stu-id="d616c-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="d616c-220">![管理](./media/active-directory-saas-itrp-tutorial/ic775576.png "管理")</span><span class="sxs-lookup"><span data-stu-id="d616c-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="d616c-221">在 新增人員 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d616c-221">On the Add New Person dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="d616c-222">![使用者](./media/active-directory-saas-itrp-tutorial/ic775577.png "使用者")</span><span class="sxs-lookup"><span data-stu-id="d616c-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="d616c-223">a.</span><span class="sxs-lookup"><span data-stu-id="d616c-223">a.</span></span> <span data-ttu-id="d616c-224">輸入您想要佈建之有效 AAD 帳戶的 [名稱]、[電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="d616c-224">Type the **Name**, **Email** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="d616c-225">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d616c-225">b.</span></span> <span data-ttu-id="d616c-226">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d616c-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="d616c-227">您可以使用任何其他的 ITRP 使用者帳戶建立工具或 ITRP 提供的 API 來佈建 AAD 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d616c-227">You can use any other ITRP user account creation tools or APIs provided by ITRP to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d616c-228">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d616c-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d616c-229">在本節中，您會將 ITRP 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d616c-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ITRP.</span></span>

![指派使用者][200] 

<span data-ttu-id="d616c-231">**若要將 Britta Simon 指派給 ITRP，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d616c-231">**To assign Britta Simon to ITRP, perform the following steps:**</span></span>

1. <span data-ttu-id="d616c-232">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d616c-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d616c-234">在應用程式清單中，選取 [ITRP]。</span><span class="sxs-lookup"><span data-stu-id="d616c-234">In the applications list, select **ITRP**.</span></span>

    ![設定單一登入](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="d616c-236">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d616c-236">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d616c-238">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d616c-238">Click **Add** button.</span></span> <span data-ttu-id="d616c-239">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d616c-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d616c-241">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d616c-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d616c-242">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d616c-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d616c-243">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d616c-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d616c-244">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d616c-244">Testing single sign-on</span></span>

<span data-ttu-id="d616c-245">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="d616c-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d616c-246">當您在存取面板中按一下 [ITRP] 圖格時，應該會自動登入您的 ITRP 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d616c-246">When you click the ITRP tile in the Access Panel, you should get automatically signed-on to your ITRP application.</span></span>
<span data-ttu-id="d616c-247">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d616c-247">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d616c-248">其他資源</span><span class="sxs-lookup"><span data-stu-id="d616c-248">Additional resources</span></span>

* [<span data-ttu-id="d616c-249">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d616c-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d616c-250">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d616c-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

