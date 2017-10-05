---
title: "教學課程：Azure Active Directory 與 Tangoe 命令高階行動裝置整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Tangoe 命令高階行動裝置之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2b0b544c-9c2c-49cd-862b-ec2ee9330126
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 595541e7248a7486e58123927389c552af0e50f7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tangoe-command-premium-mobile"></a><span data-ttu-id="56870-103">教學課程：Azure Active Directory 整合 Tangoe 命令高階行動裝置</span><span class="sxs-lookup"><span data-stu-id="56870-103">Tutorial: Azure Active Directory integration with Tangoe Command Premium Mobile</span></span>

<span data-ttu-id="56870-104">在本教學課程中，您會了解如何整合 Tangoe 命令高階行動裝置與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="56870-104">In this tutorial, you learn how to integrate Tangoe Command Premium Mobile with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="56870-105">Tangoe 命令高階行動裝置與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="56870-105">Integrating Tangoe Command Premium Mobile with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="56870-106">您可以在 Azure AD 中控制可存取 Tangoe 命令高階行動裝置的人員</span><span class="sxs-lookup"><span data-stu-id="56870-106">You can control in Azure AD who has access to Tangoe Command Premium Mobile</span></span>
- <span data-ttu-id="56870-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Tangoe 命令高階行動裝置 (單一登入)</span><span class="sxs-lookup"><span data-stu-id="56870-107">You can enable your users to automatically get signed-on to Tangoe Command Premium Mobile (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="56870-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="56870-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="56870-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="56870-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56870-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="56870-110">Prerequisites</span></span>

<span data-ttu-id="56870-111">若要設定與 Tangoe 命令高階行動裝置的 Azure AD 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="56870-111">To configure Azure AD integration with Tangoe Command Premium Mobile, you need the following items:</span></span>

- <span data-ttu-id="56870-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="56870-112">An Azure AD subscription</span></span>
- <span data-ttu-id="56870-113">已啟用 Tangoe 命令高階行動裝置單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="56870-113">A Tangoe Command Premium Mobile single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="56870-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="56870-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="56870-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="56870-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="56870-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="56870-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="56870-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="56870-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="56870-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="56870-118">Scenario description</span></span>
<span data-ttu-id="56870-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="56870-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="56870-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="56870-121">從資源庫新增 Tangoe 命令高階行動裝置</span><span class="sxs-lookup"><span data-stu-id="56870-121">Add Tangoe Command Premium Mobile from the gallery</span></span>
2. <span data-ttu-id="56870-122">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="56870-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tangoe-command-premium-mobile-from-the-gallery"></a><span data-ttu-id="56870-123">從資源庫新增 Tangoe 命令高階行動裝置</span><span class="sxs-lookup"><span data-stu-id="56870-123">Add Tangoe Command Premium Mobile from the gallery</span></span>
<span data-ttu-id="56870-124">若要設定 Tangoe 命令高階行動裝置與 Azure AD 整合，您需要從資源庫將 Tangoe 命令高階行動裝置新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="56870-124">To configure the integration of Tangoe Command Premium Mobile into Azure AD, you need to add Tangoe Command Premium Mobile from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="56870-125">**若要從資源庫新增 Tangoe 命令高階行動裝置，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56870-125">**To add Tangoe Command Premium Mobile from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="56870-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="56870-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="56870-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56870-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="56870-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56870-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="56870-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56870-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="56870-133">在搜尋方塊中，輸入 **Tangoe 命令高階行動裝置**，從結果面板選取 [Tangoe 命令高階行動裝置]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="56870-133">In the search box, type **Tangoe Command Premium Mobile**, select **Tangoe Command Premium Mobile** from result panel then click **Add** button to add the application.</span></span>

    ![<span data-ttu-id="56870-134">從資源庫新增 Tangoe 命令高階行動裝置</span><span class="sxs-lookup"><span data-stu-id="56870-134">Add Tangoe Command Premium Mobile from gallery</span></span> ](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="56870-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="56870-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="56870-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 Tangoe 命令高階行動裝置設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-136">In this section, you configure and test Azure AD single sign-on with Tangoe Command Premium Mobile based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="56870-137">若要讓單一登入運作，Azure AD 必須知道 Tangoe 命令高階行動裝置與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="56870-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Tangoe Command Premium Mobile is to a user in Azure AD.</span></span> <span data-ttu-id="56870-138">換句話說，必須在 Azure AD 使用者和 Tangoe 命令高階行動裝置中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="56870-138">In other words, a link relationship between an Azure AD user and the related user in Tangoe Command Premium Mobile needs to be established.</span></span>

<span data-ttu-id="56870-139">在 Tangoe 命令高階行動裝置中，將 Azure AD 中**使用者名稱**的值，指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="56870-139">In Tangoe Command Premium Mobile, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="56870-140">若要設定及測試對 Tangoe 命令高階行動裝置的 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="56870-140">To configure and test Azure AD single sign-on with Tangoe Command Premium Mobile, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="56870-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="56870-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="56870-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="56870-143">**[建立 Tangoe 命令高階行動裝置測試使用者](#create-a-tangoe-command-premium-mobile-test-user)** - 使 Tangoe 命令高階行動裝置中 Britta Simon 的對應項目連結到使用者在 Azure AD 中的代表身分。</span><span class="sxs-lookup"><span data-stu-id="56870-143">**[Create a Tangoe Command Premium Mobile test user](#create-a-tangoe-command-premium-mobile-test-user)** - to have a counterpart of Britta Simon in Tangoe Command Premium Mobile that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="56870-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="56870-145">**[測試單一登入](#test-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="56870-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="56870-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="56870-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="56870-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，並在您的 Tangoe 命令高階行動裝置中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tangoe Command Premium Mobile application.</span></span>

<span data-ttu-id="56870-148">**若要設定透過 Tangoe 命令高階行動裝置使用 Azure AD 單一登入功能，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56870-148">**To configure Azure AD single sign-on with Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="56870-149">在 Azure 入口網站的 [Tangoe 命令高階行動裝置] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="56870-149">In the Azure portal, on the **Tangoe Command Premium Mobile** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="56870-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![SAML 型登入](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_samlbase.png)

3. <span data-ttu-id="56870-153">在 [Tangoe 命令高階行動裝置網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="56870-153">On the **Tangoe Command Premium Mobile Domain and URLs** section, perform the following steps:</span></span>

    ![Tangoe 命令高階行動裝置網域與 URL](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_url.png)

    <span data-ttu-id="56870-155">a.</span><span class="sxs-lookup"><span data-stu-id="56870-155">a.</span></span> <span data-ttu-id="56870-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span><span class="sxs-lookup"><span data-stu-id="56870-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/startSSO.ping?PartnerIdpId=<tenant issuer>&TARGET=<target page url>`</span></span>

    <span data-ttu-id="56870-157">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="56870-157">b.</span></span> <span data-ttu-id="56870-158">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://sso.tangoe.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="56870-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://sso.tangoe.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="56870-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="56870-159">These values are not real.</span></span> <span data-ttu-id="56870-160">使用實際的回覆 URL 與登入 URL 更新這些值。</span><span class="sxs-lookup"><span data-stu-id="56870-160">Update these values with the actual  Reply URL and Sign-On URL.</span></span> <span data-ttu-id="56870-161">請連絡 [Tangoe 命令高階行動裝置客戶支援小組](https://www.tangoe.com/contact-2/)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="56870-161">Contact [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to get these values.</span></span> 

4. <span data-ttu-id="56870-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="56870-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![[SAML 簽署憑證] 區段](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_certificate.png) 

5. <span data-ttu-id="56870-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="56870-164">Click **Save** button.</span></span>

    ![[儲存] 按鈕](./media/active-directory-saas-tangoe-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="56870-166">在 [Tangoe 命令高階行動裝置] 區段中，按一下 [設定 Tangoe 命令高階行動裝置] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="56870-166">On the **Tangoe Command Premium Mobile Configuration** section, click **Configure Tangoe Command Premium Mobile** to open **Configure sign-on** window.</span></span> <span data-ttu-id="56870-167">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="56870-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![[Tangoe 命令高階行動裝置設定] 區段](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_configure.png) 

7. <span data-ttu-id="56870-169">若要為應用程式設定 SSO，請連絡 [Tangoe 命令高階行動裝置客戶支援小組](https://www.tangoe.com/contact-2/)，並提供下列資訊：</span><span class="sxs-lookup"><span data-stu-id="56870-169">To get SSO configured for your application, contact your [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) and provide the following:</span></span>

   - <span data-ttu-id="56870-170">下載的中繼資料檔案</span><span class="sxs-lookup"><span data-stu-id="56870-170">The downloaded metadata file</span></span>
   - <span data-ttu-id="56870-171">**SAML 實體識別碼**</span><span class="sxs-lookup"><span data-stu-id="56870-171">The **SAML Entity ID**</span></span>
   - <span data-ttu-id="56870-172">**SAML 單一登入服務 URL**</span><span class="sxs-lookup"><span data-stu-id="56870-172">The **SAML Single Sign-On Service URL**</span></span>
   - <span data-ttu-id="56870-173">**登出 URL**</span><span class="sxs-lookup"><span data-stu-id="56870-173">The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="56870-174">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="56870-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="56870-175">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="56870-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="56870-176">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="56870-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="56870-177">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="56870-177">Create an Azure AD test user</span></span>
<span data-ttu-id="56870-178">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="56870-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="56870-180">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56870-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="56870-181">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="56870-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-tangoe-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="56870-183">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="56870-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![[使用者和群組] -> [所有使用者]](./media/active-directory-saas-tangoe-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="56870-185">若要開啟 [使用者] 對話方塊，按一下對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="56870-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![新增使用者](./media/active-directory-saas-tangoe-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="56870-187">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="56870-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![使用者對話方塊頁面](./media/active-directory-saas-tangoe-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="56870-189">a.</span><span class="sxs-lookup"><span data-stu-id="56870-189">a.</span></span> <span data-ttu-id="56870-190">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="56870-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="56870-191">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="56870-191">b.</span></span> <span data-ttu-id="56870-192">在 [使用者名稱] 文字方塊中，輸入 BrittaSimon 的**電子郵件地址**。</span><span class="sxs-lookup"><span data-stu-id="56870-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="56870-193">c.</span><span class="sxs-lookup"><span data-stu-id="56870-193">c.</span></span> <span data-ttu-id="56870-194">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="56870-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="56870-195">d.</span><span class="sxs-lookup"><span data-stu-id="56870-195">d.</span></span> <span data-ttu-id="56870-196">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="56870-196">Click **Create**.</span></span>
 
### <a name="create-a-tangoe-command-premium-mobile-test-user"></a><span data-ttu-id="56870-197">建立 Tangoe 命令高階行動裝置測試使用者</span><span class="sxs-lookup"><span data-stu-id="56870-197">Create a Tangoe Command Premium Mobile test user</span></span>

<span data-ttu-id="56870-198">在本節中，您要在 Tangoe 命令高階行動裝置中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="56870-198">In this section, you create a user called Britta Simon in Tangoe Command Premium Mobile.</span></span> 

<span data-ttu-id="56870-199">Tangoe 命令高階行動裝置應用程式需要在應用程式中佈建所有使用者才能執行單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-199">Tangoe Command Premium Mobile application needs all the users to be provisioned in the application before doing Single Sign On.</span></span> <span data-ttu-id="56870-200">因此，請與 [Tangoe 命令高階行動裝置客戶支援小組](https://www.tangoe.com/contact-2/)合作，將所有使用者佈建到應用程式。</span><span class="sxs-lookup"><span data-stu-id="56870-200">So please work with the [Tangoe Command Premium Mobile Client support team](https://www.tangoe.com/contact-2/) to provision all these users into the application.</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="56870-201">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="56870-201">Assign the Azure AD test user</span></span>

<span data-ttu-id="56870-202">在本節中，您會把 Tangoe 命令高階行動裝置的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="56870-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tangoe Command Premium Mobile.</span></span>

![指派使用者][200] 

<span data-ttu-id="56870-204">**若要指派 Brita Simon 給 Tangoe 命令高階行動裝置，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="56870-204">**To assign Britta Simon to Tangoe Command Premium Mobile, perform the following steps:**</span></span>

1. <span data-ttu-id="56870-205">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="56870-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="56870-207">在應用程式清單中，選取 [Tangoe 命令高階行動裝置] 。</span><span class="sxs-lookup"><span data-stu-id="56870-207">In the applications list, select **Tangoe Command Premium Mobile**.</span></span>

    ![應用程式清單中的 Tangoe 命令高階行動裝置](./media/active-directory-saas-tangoe-tutorial/tutorial_tangoe_app.png) 

3. <span data-ttu-id="56870-209">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="56870-209">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="56870-211">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56870-211">Click **Add** button.</span></span> <span data-ttu-id="56870-212">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="56870-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="56870-214">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="56870-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="56870-215">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56870-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="56870-216">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="56870-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="56870-217">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="56870-217">Test single sign-on</span></span>

<span data-ttu-id="56870-218">在本節中，您會使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="56870-218">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="56870-219">當您按一下存取面版中的 [Tangoe 命令高階行動裝置] 圖格，您應該會自動登入 Tangoe 命令高階行動裝置應用程式。</span><span class="sxs-lookup"><span data-stu-id="56870-219">When you click the Tangoe Command Premium Mobile tile in the Access Panel, you should get automatically signed-on to your Tangoe Command Premium Mobile application.</span></span> <span data-ttu-id="56870-220">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="56870-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="56870-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="56870-221">Additional resources</span></span>

* [<span data-ttu-id="56870-222">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="56870-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="56870-223">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="56870-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tangoe-tutorial/tutorial_general_203.png

