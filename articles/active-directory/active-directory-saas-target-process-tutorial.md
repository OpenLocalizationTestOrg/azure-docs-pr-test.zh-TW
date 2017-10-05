---
title: "教學課程：將 Azure Active Directory 與 TargetProcess 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 TargetProcess 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7cb91628-e758-480d-a233-7a3caaaff50d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: d15931a5d430252bbd9ae342e1f8fde1a539355b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-targetprocess"></a><span data-ttu-id="b4e31-103">教學課程：將 Azure Active Directory 與 TargetProcess 整合</span><span class="sxs-lookup"><span data-stu-id="b4e31-103">Tutorial: Azure Active Directory integration with TargetProcess</span></span>

<span data-ttu-id="b4e31-104">在本教學課程中，您將了解如何整合 TalentLMS 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="b4e31-104">In this tutorial, you learn how to integrate TargetProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b4e31-105">將 TargetProcess 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="b4e31-105">Integrating TargetProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b4e31-106">您可以在 Azure AD 中控制可存取 TargetProcess 的人員</span><span class="sxs-lookup"><span data-stu-id="b4e31-106">You can control in Azure AD who has access to TargetProcess</span></span>
- <span data-ttu-id="b4e31-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 TargetProcess (單一登入)</span><span class="sxs-lookup"><span data-stu-id="b4e31-107">You can enable your users to automatically get signed-on to TargetProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b4e31-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="b4e31-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b4e31-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="b4e31-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b4e31-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b4e31-110">Prerequisites</span></span>

<span data-ttu-id="b4e31-111">若要設定 Azure AD 與 TargetProcess 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="b4e31-111">To configure Azure AD integration with TargetProcess, you need the following items:</span></span>

- <span data-ttu-id="b4e31-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b4e31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b4e31-113">已啟用 TargetProcess 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="b4e31-113">A TargetProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b4e31-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b4e31-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b4e31-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="b4e31-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b4e31-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="b4e31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b4e31-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="b4e31-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b4e31-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="b4e31-118">Scenario description</span></span>
<span data-ttu-id="b4e31-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b4e31-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="b4e31-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b4e31-121">從資源庫新增 TargetProcess</span><span class="sxs-lookup"><span data-stu-id="b4e31-121">Add TargetProcess from the gallery</span></span>
2. <span data-ttu-id="b4e31-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b4e31-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-targetprocess-from-the-gallery"></a><span data-ttu-id="b4e31-123">從資源庫新增 TargetProcess</span><span class="sxs-lookup"><span data-stu-id="b4e31-123">Add TargetProcess from the gallery</span></span>
<span data-ttu-id="b4e31-124">若要設定將 TargetProcess 整合到 Azure AD 中，您需要從資源庫將 TargetProcess 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="b4e31-124">To configure the integration of TargetProcess into Azure AD, you need to add TargetProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b4e31-125">**若要從資源庫新增 TargetProcess，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b4e31-125">**To add TargetProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b4e31-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b4e31-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b4e31-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b4e31-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="b4e31-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4e31-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="b4e31-133">在搜尋方塊中，輸入 **TargetProcess**，從結果面板中選取 [TargetProcess]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4e31-133">In the search box, type **TargetProcess**, select **TargetProcess**  from result panel then click **Add** button to add the application.</span></span>

    ![從資源庫新增 TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b4e31-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b4e31-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b4e31-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 TargetProcess 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-136">In this section, you configure and test Azure AD single sign-on with TargetProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b4e31-137">若要讓單一登入能夠運作，Azure AD 必須知道 TargetProcess 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="b4e31-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TargetProcess is to a user in Azure AD.</span></span> <span data-ttu-id="b4e31-138">換句話說，必須在 Azure AD 使用者與 TargetProcess 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b4e31-138">In other words, a link relationship between an Azure AD user and the related user in TargetProcess needs to be established.</span></span>

<span data-ttu-id="b4e31-139">在 TargetProcess 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="b4e31-139">In TargetProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b4e31-140">若要設定及測試與 TargetProcess 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="b4e31-140">To configure and test Azure AD single sign-on with TargetProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b4e31-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b4e31-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b4e31-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b4e31-143">**[建立 TargetProcess 測試使用者](#create-a-targetprocess-test-user)** - 使 TargetProcess 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="b4e31-143">**[Create a TargetProcess test user](#create-a-targetprocess-test-user)** - to have a counterpart of Britta Simon in TargetProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b4e31-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b4e31-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="b4e31-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b4e31-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="b4e31-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b4e31-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 TargetProcess 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TargetProcess application.</span></span>

<span data-ttu-id="b4e31-148">**若要設定與 TargetProcess 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b4e31-148">**To configure Azure AD single sign-on with TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="b4e31-149">在 Azure 入口網站的 [TargetProcess] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-149">In the Azure portal, on the **TargetProcess** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="b4e31-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_samlbase.png)

3. <span data-ttu-id="b4e31-153">在 [TargetProcess 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b4e31-153">On the **TargetProcess Domain and URLs** section, perform the following steps:</span></span>

    ![[TargetProcess 網域與 URL] 區段](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_url.png)

    <span data-ttu-id="b4e31-155">a.</span><span class="sxs-lookup"><span data-stu-id="b4e31-155">a.</span></span> <span data-ttu-id="b4e31-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="b4e31-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    <span data-ttu-id="b4e31-157">b.</span><span class="sxs-lookup"><span data-stu-id="b4e31-157">b.</span></span> <span data-ttu-id="b4e31-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.tpondemand.com/`</span><span class="sxs-lookup"><span data-stu-id="b4e31-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.tpondemand.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b4e31-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="b4e31-159">These values are not real.</span></span> <span data-ttu-id="b4e31-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="b4e31-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b4e31-161">請連絡 [TargetProcess 客戶支援小組](mailto:support@targetprocess.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="b4e31-161">Contact [TargetProcess Client support team](mailto:support@targetprocess.com) to get these values.</span></span> 
 
4. <span data-ttu-id="b4e31-162">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="b4e31-162">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_certificate.png) 

5. <span data-ttu-id="b4e31-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4e31-164">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-target-process-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b4e31-166">在 [TargetProcess 組態] 區段上，按一下 [設定 TargetProcess] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b4e31-166">On the **TargetProcess Configuration** section, click **Configure TargetProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b4e31-167">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![[TargetProcess 組態] 區段](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_configure.png) 

7. <span data-ttu-id="b4e31-169">以系統管理員身分登入您的 TargetProcess 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4e31-169">Sign-on to your TargetProcess application as an administrator.</span></span>

8. <span data-ttu-id="b4e31-170">在頂端的功能表中，按一下 [安裝] 。</span><span class="sxs-lookup"><span data-stu-id="b4e31-170">In the menu on the top, click **Setup**.</span></span>
   
    ![設定](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_05.png)

9. <span data-ttu-id="b4e31-172">按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="b4e31-172">Click **Settings**.</span></span>
   
    ![設定](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_06.png) 

10. <span data-ttu-id="b4e31-174">按一下 [單一登入] 。</span><span class="sxs-lookup"><span data-stu-id="b4e31-174">Click **Single Sign-on**.</span></span>
   
    ![按一下 [單一登入]](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_07.png) 

11. <span data-ttu-id="b4e31-176">在 [單一登入設定] 對話方塊上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b4e31-176">On the Single Sign-on settings dialog, perform the following steps:</span></span>
   
    ![設定單一登入](./media/active-directory-saas-target-process-tutorial/tutorial_target_process_08.png)
    
    <span data-ttu-id="b4e31-178">a.</span><span class="sxs-lookup"><span data-stu-id="b4e31-178">a.</span></span> <span data-ttu-id="b4e31-179">按一下 [啟用單一登入]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-179">Click **Enable Single Sign-on**.</span></span>
    
    <span data-ttu-id="b4e31-180">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4e31-180">b.</span></span> <span data-ttu-id="b4e31-181">在 [登入 URL] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="b4e31-181">In **Sign-on URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b4e31-182">c.</span><span class="sxs-lookup"><span data-stu-id="b4e31-182">c.</span></span> <span data-ttu-id="b4e31-183">在記事本中開啟下載的憑證，複製其內容，然後貼到 [憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="b4e31-183">Open your downloaded certificate in notepad, copy the content, and then paste it into the **Certificate** textbox.</span></span>
    
    <span data-ttu-id="b4e31-184">d.</span><span class="sxs-lookup"><span data-stu-id="b4e31-184">d.</span></span> <span data-ttu-id="b4e31-185">按一下 [ **啟用 JIT 佈建**]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-185">click **Enable JIT Provisioning**.</span></span>

    <span data-ttu-id="b4e31-186">e.</span><span class="sxs-lookup"><span data-stu-id="b4e31-186">e.</span></span> <span data-ttu-id="b4e31-187">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b4e31-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b4e31-188">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="b4e31-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b4e31-189">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="b4e31-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b4e31-190">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b4e31-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b4e31-191">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b4e31-191">Create an Azure AD test user</span></span>
<span data-ttu-id="b4e31-192">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="b4e31-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="b4e31-194">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b4e31-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b4e31-195">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="b4e31-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-target-process-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b4e31-197">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![顯示使用者清單](./media/active-directory-saas-target-process-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b4e31-199">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![[新增] 按鈕](./media/active-directory-saas-target-process-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b4e31-201">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b4e31-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![[使用者] 區段](./media/active-directory-saas-target-process-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b4e31-203">a.</span><span class="sxs-lookup"><span data-stu-id="b4e31-203">a.</span></span> <span data-ttu-id="b4e31-204">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="b4e31-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b4e31-205">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4e31-205">b.</span></span> <span data-ttu-id="b4e31-206">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="b4e31-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b4e31-207">c.</span><span class="sxs-lookup"><span data-stu-id="b4e31-207">c.</span></span> <span data-ttu-id="b4e31-208">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="b4e31-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b4e31-209">d.</span><span class="sxs-lookup"><span data-stu-id="b4e31-209">d.</span></span> <span data-ttu-id="b4e31-210">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="b4e31-210">Click **Create**.</span></span>
 
### <a name="create-a-targetprocess-test-user"></a><span data-ttu-id="b4e31-211">建立 TargetProcess 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b4e31-211">Create a TargetProcess test user</span></span>

<span data-ttu-id="b4e31-212">本節的目標是要在 TargetProcess 中建立一個名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="b4e31-212">The objective of this section is to create a user called Britta Simon in TargetProcess.</span></span>

<span data-ttu-id="b4e31-213">TargetProcess 支援 Just-in-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="b4e31-213">TargetProcess supports just-in-time provisioning.</span></span> <span data-ttu-id="b4e31-214">您已在 [設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)中啟用。</span><span class="sxs-lookup"><span data-stu-id="b4e31-214">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="b4e31-215">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="b4e31-215">There is no action item for you in this section.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="b4e31-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="b4e31-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="b4e31-217">在本節中，您會將 TargetProcess 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="b4e31-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TargetProcess.</span></span>

![指派使用者][200] 

<span data-ttu-id="b4e31-219">**若要將 Britta Simon 指派給 TargetProcess，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="b4e31-219">**To assign Britta Simon to TargetProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="b4e31-220">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="b4e31-222">在應用程式清單中，選取 [TargetProcess] 。</span><span class="sxs-lookup"><span data-stu-id="b4e31-222">In the applications list, select **TargetProcess**.</span></span>

    ![應用程式清單中的 TargetProcess](./media/active-directory-saas-target-process-tutorial/tutorial_target-process_app.png) 

3. <span data-ttu-id="b4e31-224">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-224">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="b4e31-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4e31-226">Click **Add** button.</span></span> <span data-ttu-id="b4e31-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="b4e31-229">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="b4e31-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b4e31-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4e31-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b4e31-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b4e31-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b4e31-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="b4e31-232">Test single sign-on</span></span>

<span data-ttu-id="b4e31-233">本節的目標是要使用「存取面板」來測試您的 Azure AD 單一登入組態。</span><span class="sxs-lookup"><span data-stu-id="b4e31-233">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b4e31-234">當您在存取面板中按一下 TargetProcess 磚時，應該會自動登入您的 TargetProcess 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b4e31-234">When you click the TargetProcess tile in the Access Panel, you should get automatically signed-on to your TargetProcess application.</span></span> <span data-ttu-id="b4e31-235">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="b4e31-235">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b4e31-236">其他資源</span><span class="sxs-lookup"><span data-stu-id="b4e31-236">Additional resources</span></span>

* [<span data-ttu-id="b4e31-237">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="b4e31-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b4e31-238">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="b4e31-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-target-process-tutorial/tutorial_general_203.png

