---
title: "教學課程：Azure Active Directory 與 LiquidFiles 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 LiquidFiles 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cb517134-0b34-4a74-b40c-5a3223ca81b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: b858c6d26b78be4641a46b3453f53d103b512356
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-liquidfiles"></a><span data-ttu-id="d7d21-103">教學課程：Azure Active Directory 與 LiquidFiles 整合</span><span class="sxs-lookup"><span data-stu-id="d7d21-103">Tutorial: Azure Active Directory integration with LiquidFiles</span></span>

<span data-ttu-id="d7d21-104">在本教學課程中，您會了解如何整合 LiquidFiles 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="d7d21-104">In this tutorial, you learn how to integrate LiquidFiles with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d7d21-105">LiquidFiles 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="d7d21-105">Integrating LiquidFiles with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d7d21-106">您可以在 Azure AD 中控制可存取 LiquidFiles 的人員</span><span class="sxs-lookup"><span data-stu-id="d7d21-106">You can control in Azure AD who has access to LiquidFiles</span></span>
- <span data-ttu-id="d7d21-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 LiquidFiles (單一登入)</span><span class="sxs-lookup"><span data-stu-id="d7d21-107">You can enable your users to automatically get signed-on to LiquidFiles (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d7d21-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="d7d21-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d7d21-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="d7d21-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d7d21-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="d7d21-110">Prerequisites</span></span>

<span data-ttu-id="d7d21-111">若要設定 Azure AD 與 LiquidFiles 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="d7d21-111">To configure Azure AD integration with LiquidFiles, you need the following items:</span></span>

- <span data-ttu-id="d7d21-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d7d21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d7d21-113">啟用 LiquidFiles 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d7d21-113">A LiquidFiles single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d7d21-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d7d21-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d7d21-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="d7d21-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d7d21-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="d7d21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d7d21-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="d7d21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d7d21-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="d7d21-118">Scenario description</span></span>
<span data-ttu-id="d7d21-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d7d21-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="d7d21-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d7d21-121">從資源庫新增 LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="d7d21-121">Adding LiquidFiles from the gallery</span></span>
2. <span data-ttu-id="d7d21-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d7d21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-liquidfiles-from-the-gallery"></a><span data-ttu-id="d7d21-123">從資源庫新增 LiquidFiles</span><span class="sxs-lookup"><span data-stu-id="d7d21-123">Adding LiquidFiles from the gallery</span></span>
<span data-ttu-id="d7d21-124">若要設定將 LiquidFiles 整合到 Azure AD 中，您需要從資源庫將 LiquidFiles 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="d7d21-124">To configure the integration of LiquidFiles into Azure AD, you need to add LiquidFiles from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d7d21-125">**若要從資源庫新增 LiquidFiles，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d7d21-125">**To add LiquidFiles from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d7d21-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d7d21-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d7d21-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d7d21-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="d7d21-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7d21-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="d7d21-133">在搜尋方塊中，輸入 **LiquidFiles**。</span><span class="sxs-lookup"><span data-stu-id="d7d21-133">In the search box, type **LiquidFiles**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_search.png)

5. <span data-ttu-id="d7d21-135">在結果面板中，選取 [LiquidFiles]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7d21-135">In the results panel, select **LiquidFiles**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d7d21-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d7d21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d7d21-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 LiquidFiles 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-138">In this section, you configure and test Azure AD single sign-on with LiquidFiles based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d7d21-139">若要讓單一登入運作，Azure AD 必須知道 LiquidFiles 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="d7d21-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LiquidFiles is to a user in Azure AD.</span></span> <span data-ttu-id="d7d21-140">換句話說，必須在 Azure AD 使用者和 LiquidFiles 中的相關使用者之間，建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d7d21-140">In other words, a link relationship between an Azure AD user and the related user in LiquidFiles needs to be established.</span></span>

<span data-ttu-id="d7d21-141">在 LiquidFiles 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="d7d21-141">In LiquidFiles, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d7d21-142">若要設定及測試與 LiquidFiles 搭配運作的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="d7d21-142">To configure and test Azure AD single sign-on with LiquidFiles, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d7d21-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="d7d21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d7d21-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d7d21-145">**[建立 LiquidFiles 測試使用者](#creating-a-liquidfiles-test-user)** - 使用 LiquidFiles 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="d7d21-145">**[Creating a LiquidFiles test user](#creating-a-liquidfiles-test-user)** - to have a counterpart of Britta Simon in LiquidFiles that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d7d21-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d7d21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="d7d21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d7d21-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="d7d21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d7d21-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 LiquidFiles 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LiquidFiles application.</span></span>

<span data-ttu-id="d7d21-150">**若要設定與 LiquidFiles 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d7d21-150">**To configure Azure AD single sign-on with LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="d7d21-151">在 Azure 入口網站的 [LiquidFiles] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-151">In the Azure portal, on the **LiquidFiles** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="d7d21-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_samlbase.png)

3. <span data-ttu-id="d7d21-155">在 [LiquidFiles 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d7d21-155">On the **LiquidFiles Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_url.png)

    <span data-ttu-id="d7d21-157">a.</span><span class="sxs-lookup"><span data-stu-id="d7d21-157">a.</span></span> <span data-ttu-id="d7d21-158">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<YOUR_SERVER_URL>/saml/init`</span><span class="sxs-lookup"><span data-stu-id="d7d21-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/init`</span></span>

    <span data-ttu-id="d7d21-159">b.</span><span class="sxs-lookup"><span data-stu-id="d7d21-159">b.</span></span> <span data-ttu-id="d7d21-160">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<YOUR_SERVER_URL>`</span><span class="sxs-lookup"><span data-stu-id="d7d21-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>`</span></span>

    <span data-ttu-id="d7d21-161">c.</span><span class="sxs-lookup"><span data-stu-id="d7d21-161">c.</span></span> <span data-ttu-id="d7d21-162">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7d21-162">b.</span></span> <span data-ttu-id="d7d21-163">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<YOUR_SERVER_URL>/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="d7d21-163">In the **Reply URL** textbox, type a URL using the following pattern: `https://<YOUR_SERVER_URL>/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d7d21-164">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-164">These values are not real.</span></span> <span data-ttu-id="d7d21-165">請使用實際的「登入 URL」、「識別碼」及「回覆 URL」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-165">Update these values with the actual Sign-On URL, Identifier and, Reply URL.</span></span> <span data-ttu-id="d7d21-166">請連絡 [LiquidFiles 客戶支援小組](https://www.liquidfiles.com/support.html)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-166">Contact [LiquidFiles Client support team](https://www.liquidfiles.com/support.html) to get these values.</span></span> 
 
4. <span data-ttu-id="d7d21-167">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-167">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_certificate.png) 

5. <span data-ttu-id="d7d21-169">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7d21-169">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d7d21-171">在 [LiquidFiles 組態] 區段上，按一下 [設定 LiquidFiles] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d7d21-171">On the **LiquidFiles Configuration** section, click **Configure LiquidFiles** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d7d21-172">從 [快速參考] 區段中複製 [登入 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-172">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_configure.png)
 
7. <span data-ttu-id="d7d21-174">以系統管理員身分登入您的 LiquidFiles 公司網站。</span><span class="sxs-lookup"><span data-stu-id="d7d21-174">Sign-on to your LiquidFiles company site as administrator.</span></span>

8. <span data-ttu-id="d7d21-175">從功能表中，在 [管理 > 設定] 中按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-175">Click **Single Sign-On** in the **Admin > Configuration** from the menu.</span></span>

9. <span data-ttu-id="d7d21-176">在 [單一登入設定] 頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d7d21-176">On the **Single Sign-On Configuration** page, perform the following steps</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_single_01.png)

    <span data-ttu-id="d7d21-178">a.</span><span class="sxs-lookup"><span data-stu-id="d7d21-178">a.</span></span> <span data-ttu-id="d7d21-179">在 [單一登入方法] 中，選取 [SAML 2]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-179">As **Single Sign On Method**, select **SAML 2**.</span></span>

    <span data-ttu-id="d7d21-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7d21-180">b.</span></span> <span data-ttu-id="d7d21-181">在 [IDP 登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-181">In the **IDP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d7d21-182">c.</span><span class="sxs-lookup"><span data-stu-id="d7d21-182">c.</span></span> <span data-ttu-id="d7d21-183">在 [IDP 登出 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-183">In the **IDP Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d7d21-184">d.</span><span class="sxs-lookup"><span data-stu-id="d7d21-184">d.</span></span> <span data-ttu-id="d7d21-185">在 [IDP 憑證指紋] 文字方塊中，貼上您從 Azure 入口網站複製的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-185">In the **IDP Cert Fingerprint** textbox, paste the **THUMBPRINT** value which you have copied from Azure portal..</span></span>

    <span data-ttu-id="d7d21-186">e.</span><span class="sxs-lookup"><span data-stu-id="d7d21-186">e.</span></span> <span data-ttu-id="d7d21-187">在 [名稱識別碼格式] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**。</span><span class="sxs-lookup"><span data-stu-id="d7d21-187">In the Name Identifier Format textbox, type the value **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="d7d21-188">f.</span><span class="sxs-lookup"><span data-stu-id="d7d21-188">f.</span></span> <span data-ttu-id="d7d21-189">在 [驗證內容] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**。</span><span class="sxs-lookup"><span data-stu-id="d7d21-189">In the Authn Context textbox, type the value **urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport**.</span></span>

    <span data-ttu-id="d7d21-190">g.</span><span class="sxs-lookup"><span data-stu-id="d7d21-190">g.</span></span> <span data-ttu-id="d7d21-191">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="d7d21-191">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="d7d21-192">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="d7d21-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d7d21-193">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="d7d21-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d7d21-194">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d7d21-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d7d21-195">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d7d21-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="d7d21-196">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="d7d21-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="d7d21-198">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d7d21-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d7d21-199">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d7d21-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d7d21-201">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d7d21-203">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d7d21-205">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="d7d21-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-liquidfiles-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d7d21-207">a.</span><span class="sxs-lookup"><span data-stu-id="d7d21-207">a.</span></span> <span data-ttu-id="d7d21-208">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="d7d21-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d7d21-209">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7d21-209">b.</span></span> <span data-ttu-id="d7d21-210">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="d7d21-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d7d21-211">c.</span><span class="sxs-lookup"><span data-stu-id="d7d21-211">c.</span></span> <span data-ttu-id="d7d21-212">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="d7d21-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d7d21-213">d.</span><span class="sxs-lookup"><span data-stu-id="d7d21-213">d.</span></span> <span data-ttu-id="d7d21-214">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="d7d21-214">Click **Create**.</span></span>
 
### <a name="creating-a-liquidfiles-test-user"></a><span data-ttu-id="d7d21-215">建立 LiquidFiles 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d7d21-215">Creating a LiquidFiles test user</span></span>

<span data-ttu-id="d7d21-216">本節的目標是要在 LiquidFiles 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="d7d21-216">The objective of this section is to create a user called Britta Simon in LiquidFiles.</span></span> <span data-ttu-id="d7d21-217">在登入您的 LiquidFiles 應用程式之前，請與 LiquidFiles 伺服器管理員合作，將您自己新增為使用者。</span><span class="sxs-lookup"><span data-stu-id="d7d21-217">Work with your LiquidFiles server administrator to get yourself added as a user before logging in to your LiquidFiles application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d7d21-218">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="d7d21-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d7d21-219">在本節中，您會將 LiquidFiles 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="d7d21-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LiquidFiles.</span></span>

![指派使用者][200] 

<span data-ttu-id="d7d21-221">**若要將 Britta Simon 指派給 LiquidFiles，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="d7d21-221">**To assign Britta Simon to LiquidFiles, perform the following steps:**</span></span>

1. <span data-ttu-id="d7d21-222">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="d7d21-224">在應用程式清單中，選取 [LiquidFiles]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-224">In the applications list, select **LiquidFiles**.</span></span>

    ![設定單一登入](./media/active-directory-saas-liquidfiles-tutorial/tutorial_liquidfiles_app.png) 

3. <span data-ttu-id="d7d21-226">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-226">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="d7d21-228">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7d21-228">Click **Add** button.</span></span> <span data-ttu-id="d7d21-229">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="d7d21-231">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="d7d21-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d7d21-232">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7d21-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d7d21-233">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d7d21-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d7d21-234">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="d7d21-234">Testing single sign-on</span></span>

<span data-ttu-id="d7d21-235">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="d7d21-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d7d21-236">當您在存取面板中按一下 LiquidFiles 圖格時，應該會自動登入您的 LiquidFiles 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d7d21-236">When you click the LiquidFiles tile in the Access Panel, you should get automatically signed-on to your LiquidFiles application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d7d21-237">其他資源</span><span class="sxs-lookup"><span data-stu-id="d7d21-237">Additional resources</span></span>

* [<span data-ttu-id="d7d21-238">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="d7d21-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d7d21-239">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="d7d21-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-liquidfiles-tutorial/tutorial_general_203.png

