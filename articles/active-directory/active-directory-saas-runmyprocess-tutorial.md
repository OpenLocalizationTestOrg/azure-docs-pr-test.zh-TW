---
title: "教學課程：Azure Active Directory 與 RunMyProcess 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 RunMyProcess 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d31f7395-048b-4a61-9505-5acf9fc68d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: f8a08ef4f90d5cb98e7648ae6001055a3f4696e8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-runmyprocess"></a><span data-ttu-id="27bd5-103">教學課程：Azure Active Directory 與 RunMyProcess 整合</span><span class="sxs-lookup"><span data-stu-id="27bd5-103">Tutorial: Azure Active Directory integration with RunMyProcess</span></span>

<span data-ttu-id="27bd5-104">在本教學課程中，您會了解如何整合 RunMyProcess 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="27bd5-104">In this tutorial, you learn how to integrate RunMyProcess with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="27bd5-105">RunMyProcess 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="27bd5-105">Integrating RunMyProcess with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="27bd5-106">您可以在 Azure AD 中控制可存取 RunMyProcess 的人員</span><span class="sxs-lookup"><span data-stu-id="27bd5-106">You can control in Azure AD who has access to RunMyProcess</span></span>
- <span data-ttu-id="27bd5-107">您可以讓您的使用者使用他們的 Azure AD 帳戶自動登入 RunMyProcess (單一登入)</span><span class="sxs-lookup"><span data-stu-id="27bd5-107">You can enable your users to automatically get signed-on to RunMyProcess (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="27bd5-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="27bd5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="27bd5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="27bd5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27bd5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="27bd5-110">Prerequisites</span></span>

<span data-ttu-id="27bd5-111">若要設定 Azure AD 與 RunMyProcess 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="27bd5-111">To configure Azure AD integration with RunMyProcess, you need the following items:</span></span>

- <span data-ttu-id="27bd5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27bd5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="27bd5-113">啟用 RunMyProcess 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="27bd5-113">A RunMyProcess single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="27bd5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="27bd5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="27bd5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="27bd5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="27bd5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="27bd5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="27bd5-117">如果您沒有 Azure AD 試用環境，您可以在這裡取得一個月試用：[試用優惠](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="27bd5-117">If you don't have an Azure AD trial environment, you can get a one-month trial here:[Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="27bd5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="27bd5-118">Scenario description</span></span>
<span data-ttu-id="27bd5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="27bd5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="27bd5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="27bd5-121">從資源庫新增 RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="27bd5-121">Adding RunMyProcess from the gallery</span></span>
2. <span data-ttu-id="27bd5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27bd5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-runmyprocess-from-the-gallery"></a><span data-ttu-id="27bd5-123">從資源庫新增 RunMyProcess</span><span class="sxs-lookup"><span data-stu-id="27bd5-123">Adding RunMyProcess from the gallery</span></span>
<span data-ttu-id="27bd5-124">若要設定將 RunMyProcess 整合到 Azure AD 中，您需要從資源庫將 RunMyProcess 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="27bd5-124">To configure the integration of RunMyProcess into Azure AD, you need to add RunMyProcess from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="27bd5-125">**若要從資源庫新增 RunMyProces，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27bd5-125">**To add RunMyProcess from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="27bd5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="27bd5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="27bd5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="27bd5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="27bd5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27bd5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="27bd5-133">在搜尋方塊中，輸入 **RunMyProcess**。</span><span class="sxs-lookup"><span data-stu-id="27bd5-133">In the search box, type **RunMyProcess**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_search.png)

5. <span data-ttu-id="27bd5-135">在結果面板中，選取 [RunMyProcess]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="27bd5-135">In the results panel, select **RunMyProcess**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="27bd5-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27bd5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="27bd5-138">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 RunMyProcess 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-138">In this section, you configure and test Azure AD single sign-on with RunMyProcess based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="27bd5-139">若要讓單一登入能夠運作，Azure AD 必須知道 RunMyProcess 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="27bd5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RunMyProcess is to a user in Azure AD.</span></span> <span data-ttu-id="27bd5-140">換句話說，必須在 Azure AD 使用者和 RunMyProcess 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="27bd5-140">In other words, a link relationship between an Azure AD user and the related user in RunMyProcess needs to be established.</span></span>

<span data-ttu-id="27bd5-141">在 RunMyProcess 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="27bd5-141">In RunMyProcess, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="27bd5-142">若要設定及測試透過 RunMyProcess 使用 Azure AD 單一登入功能，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="27bd5-142">To configure and test Azure AD single sign-on with RunMyProcess, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="27bd5-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="27bd5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="27bd5-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="27bd5-145">**[建立 RunMyProcess 測試使用者](#creating-a-runmyprocess-test-user)** - 使 RunMyProcess 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="27bd5-145">**[Creating a RunMyProcess test user](#creating-a-runmyprocess-test-user)** - to have a counterpart of Britta Simon in RunMyProcess that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="27bd5-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="27bd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="27bd5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="27bd5-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="27bd5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="27bd5-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 RunMyProcess 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RunMyProcess application.</span></span>

<span data-ttu-id="27bd5-150">**若要設定透過 RunMyProcess 使用 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27bd5-150">**To configure Azure AD single sign-on with RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="27bd5-151">在 Azure 入口網站的 [RunMyProcess] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-151">In the Azure portal, on the **RunMyProcess** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="27bd5-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_samlbase.png)

3. <span data-ttu-id="27bd5-155">在 [RunMyProcess 網域及 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="27bd5-155">On the **RunMyProcess Domain and URLs** section, perform the following steps:</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_url.png)

    <span data-ttu-id="27bd5-157">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://live.runmyprocess.com/live/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="27bd5-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://live.runmyprocess.com/live/<tenant id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="27bd5-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-158">The value is not real.</span></span> <span data-ttu-id="27bd5-159">請使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="27bd5-160">請連絡 [RunMyProcess 客戶支援小組](mailto:support@runmyprocess.com)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-160">Contact [RunMyProcess Client support team](mailto:support@runmyprocess.com) to get the value.</span></span> 

4. <span data-ttu-id="27bd5-161">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="27bd5-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_certificate.png) 

5. <span data-ttu-id="27bd5-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="27bd5-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="27bd5-165">在 [RunMyProcess 組態] 區段上，按一下 [設定 RunMyProcess] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="27bd5-165">On the **RunMyProcess Configuration** section, click **Configure RunMyProcess** to open **Configure sign-on** window.</span></span> <span data-ttu-id="27bd5-166">從 [快速參考] 區段中複製 [登入 URL] 和 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_configure.png) 

7. <span data-ttu-id="27bd5-168">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 RunMyProcess 租用戶。</span><span class="sxs-lookup"><span data-stu-id="27bd5-168">In a different web browser window, sign-on to your RunMyProcess tenant as an administrator.</span></span>

8. <span data-ttu-id="27bd5-169">在左方瀏覽面板中，按一下 [帳戶]，然後選取 [組態]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-169">In left navigation panel, click **Account** and select **Configuration**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_001.png)

9. <span data-ttu-id="27bd5-171">移至 [驗證方法] 區段並執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="27bd5-171">Go to **Authentication method** section and perform below steps:</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_002.png)

    <span data-ttu-id="27bd5-173">a.</span><span class="sxs-lookup"><span data-stu-id="27bd5-173">a.</span></span> <span data-ttu-id="27bd5-174">在 [方法]，選取 [使用 Samlv2 進行 SSO]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-174">As **Method**, select **SSO with Samlv2**.</span></span> 

    <span data-ttu-id="27bd5-175">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="27bd5-175">b.</span></span> <span data-ttu-id="27bd5-176">在 [SSO 重新導向] 文字方塊中，貼上您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-176">In the **SSO redirect** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="27bd5-177">c.</span><span class="sxs-lookup"><span data-stu-id="27bd5-177">c.</span></span> <span data-ttu-id="27bd5-178">在 [登出重新導向] 文字方塊中，貼上您從 Azure 入口網站複製的 [登出 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-178">In the **Logout redirect** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="27bd5-179">d.</span><span class="sxs-lookup"><span data-stu-id="27bd5-179">d.</span></span> <span data-ttu-id="27bd5-180">在 [名稱識別碼格式] 文字方塊中，輸入 **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress** 作為**名稱識別碼格式**的值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-180">In the **Name Id Format** textbox, type the value of **Name Identifier Format** as **urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress**.</span></span>

    <span data-ttu-id="27bd5-181">e.</span><span class="sxs-lookup"><span data-stu-id="27bd5-181">e.</span></span> <span data-ttu-id="27bd5-182">複製所下載憑證檔案的內容，然後將它貼至 [憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="27bd5-182">Copy the content of the downloaded certificate file and then paste it into the **Certificate** textbox.</span></span> 
 
    <span data-ttu-id="27bd5-183">f.</span><span class="sxs-lookup"><span data-stu-id="27bd5-183">f.</span></span> <span data-ttu-id="27bd5-184">按一下 [儲存]  圖示。</span><span class="sxs-lookup"><span data-stu-id="27bd5-184">Click **Save** icon.</span></span>

> [!TIP]
> <span data-ttu-id="27bd5-185">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="27bd5-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="27bd5-186">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="27bd5-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="27bd5-187">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="27bd5-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="27bd5-188">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27bd5-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="27bd5-189">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="27bd5-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="27bd5-191">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27bd5-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="27bd5-192">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="27bd5-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="27bd5-194">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="27bd5-196">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="27bd5-198">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="27bd5-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-runmyprocess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="27bd5-200">a.</span><span class="sxs-lookup"><span data-stu-id="27bd5-200">a.</span></span> <span data-ttu-id="27bd5-201">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="27bd5-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="27bd5-202">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="27bd5-202">b.</span></span> <span data-ttu-id="27bd5-203">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="27bd5-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="27bd5-204">c.</span><span class="sxs-lookup"><span data-stu-id="27bd5-204">c.</span></span> <span data-ttu-id="27bd5-205">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="27bd5-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="27bd5-206">d.</span><span class="sxs-lookup"><span data-stu-id="27bd5-206">d.</span></span> <span data-ttu-id="27bd5-207">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="27bd5-207">Click **Create**.</span></span>
 
### <a name="creating-a-runmyprocess-test-user"></a><span data-ttu-id="27bd5-208">建立 RunMyProcess 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27bd5-208">Creating a RunMyProcess test user</span></span>

<span data-ttu-id="27bd5-209">若要讓 Azure AD 使用者能夠登入 RunMyProcess，必須將他們佈建到 RunMyProcess。</span><span class="sxs-lookup"><span data-stu-id="27bd5-209">In order to enable Azure AD users to log in to RunMyProcess, they must be provisioned into RunMyProcess.</span></span> <span data-ttu-id="27bd5-210">RunMyProcess 需以手動的方式佈建。</span><span class="sxs-lookup"><span data-stu-id="27bd5-210">In the case of RunMyProcess, provisioning is a manual task.</span></span>

<span data-ttu-id="27bd5-211">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27bd5-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="27bd5-212">以系統管理員身分登入您的 RunMyProcess 公司網站。</span><span class="sxs-lookup"><span data-stu-id="27bd5-212">Log in to your RunMyProcess company site as an administrator.</span></span>

2. <span data-ttu-id="27bd5-213">按一下 [帳戶] 並選取 [使用者]，然後按一下 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-213">Click **Account** and select **Users** in left navigation panel, then click **New User**.</span></span>
   
    <span data-ttu-id="27bd5-214">![新增使用者](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "新增使用者")</span><span class="sxs-lookup"><span data-stu-id="27bd5-214">![New User](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_003.png "New User")</span></span>

3. <span data-ttu-id="27bd5-215">在 [使用者設定]  區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="27bd5-215">In the **User Settings** section, perform the following steps:</span></span>
   
    <span data-ttu-id="27bd5-216">![設定檔](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "設定檔")</span><span class="sxs-lookup"><span data-stu-id="27bd5-216">![Profile](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_004.png "Profile")</span></span> 
  
    <span data-ttu-id="27bd5-217">a.</span><span class="sxs-lookup"><span data-stu-id="27bd5-217">a.</span></span> <span data-ttu-id="27bd5-218">在相關的文字方塊中，輸入您想要佈建之有效 Azure AD 帳戶的 [名稱] 和 [電子郵件]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-218">Type the **Name** and **E-mail** of a valid Azure AD account you want to provision into the related textboxes.</span></span> 

    <span data-ttu-id="27bd5-219">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="27bd5-219">b.</span></span> <span data-ttu-id="27bd5-220">選取 [IDE 語言]、[語言] 和 [設定檔]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-220">Select an **IDE language**, **Language**, and **Profile**.</span></span> 

    <span data-ttu-id="27bd5-221">c.</span><span class="sxs-lookup"><span data-stu-id="27bd5-221">c.</span></span> <span data-ttu-id="27bd5-222">選取 [傳送帳戶建立電子郵件給我] 。</span><span class="sxs-lookup"><span data-stu-id="27bd5-222">Select **Send account creation e-mail to me**.</span></span> 

    <span data-ttu-id="27bd5-223">d.</span><span class="sxs-lookup"><span data-stu-id="27bd5-223">d.</span></span> <span data-ttu-id="27bd5-224">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="27bd5-224">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="27bd5-225">您可以使用任何其他的 RunMyProcess 使用者帳戶建立工具或 RunMyProcess 提供的 API 來佈建 Azure Active Directory 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="27bd5-225">You can use any other RunMyProcess user account creation tools or APIs provided by RunMyProcess to provision Azure Active Directory user accounts.</span></span> 
    > 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="27bd5-226">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="27bd5-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="27bd5-227">在本節中，您會將 RunMyProcess 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="27bd5-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RunMyProcess.</span></span>

![指派使用者][200] 

<span data-ttu-id="27bd5-229">**若要將 Britta Simon 指派給 RunMyProcess，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="27bd5-229">**To assign Britta Simon to RunMyProcess, perform the following steps:**</span></span>

1. <span data-ttu-id="27bd5-230">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="27bd5-232">在應用程式清單中，選取 [RunMyProcess]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-232">In the applications list, select **RunMyProcess**.</span></span>

    ![設定單一登入](./media/active-directory-saas-runmyprocess-tutorial/tutorial_runmyprocess_app.png) 

3. <span data-ttu-id="27bd5-234">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-234">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="27bd5-236">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27bd5-236">Click **Add** button.</span></span> <span data-ttu-id="27bd5-237">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="27bd5-239">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="27bd5-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="27bd5-240">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27bd5-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="27bd5-241">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="27bd5-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="27bd5-242">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="27bd5-242">Testing single sign-on</span></span>

<span data-ttu-id="27bd5-243">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="27bd5-243">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="27bd5-244">當您在存取面板中按一下 RunMyProcess 圖格時，應該會自動登入您的 RunMyProcess 應用程式。</span><span class="sxs-lookup"><span data-stu-id="27bd5-244">When you click the RunMyProcess tile in the Access Panel, you should get automatically signed-on to your RunMyProcess application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="27bd5-245">其他資源</span><span class="sxs-lookup"><span data-stu-id="27bd5-245">Additional resources</span></span>

* [<span data-ttu-id="27bd5-246">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="27bd5-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="27bd5-247">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="27bd5-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-runmyprocess-tutorial/tutorial_general_203.png

