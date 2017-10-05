---
title: "教學課程：Azure Active Directory 與 Front 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Front 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 88270b6d-2571-434a-b139-b6ccc3a2b19f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: d936bc50a66ac2a3c17038ff08351edf9902c99f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-front"></a><span data-ttu-id="4734a-103">教學課程：Azure Active Directory 與 Front 整合</span><span class="sxs-lookup"><span data-stu-id="4734a-103">Tutorial: Azure Active Directory integration with Front</span></span>

<span data-ttu-id="4734a-104">在本教學課程中，您將了解如何整合 Front 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="4734a-104">In this tutorial, you learn how to integrate Front with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4734a-105">將 Front 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="4734a-105">Integrating Front with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4734a-106">您可以在 Azure AD 中控制可存取 Front 的人員。</span><span class="sxs-lookup"><span data-stu-id="4734a-106">You can control in Azure AD who has access to Front.</span></span>
- <span data-ttu-id="4734a-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Front (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="4734a-107">You can enable your users to automatically get signed-on to Front (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4734a-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4734a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="4734a-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="4734a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4734a-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="4734a-110">Prerequisites</span></span>

<span data-ttu-id="4734a-111">若要設定 Azure AD 與 Front 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="4734a-111">To configure Azure AD integration with Front, you need the following items:</span></span>

- <span data-ttu-id="4734a-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4734a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4734a-113">已啟用 Front 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4734a-113">A Front single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4734a-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4734a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4734a-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="4734a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4734a-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="4734a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4734a-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4734a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4734a-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="4734a-118">Scenario description</span></span>
<span data-ttu-id="4734a-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4734a-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="4734a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4734a-121">從資源庫新增 Front</span><span class="sxs-lookup"><span data-stu-id="4734a-121">Adding Front from the gallery</span></span>
2. <span data-ttu-id="4734a-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4734a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-front-from-the-gallery"></a><span data-ttu-id="4734a-123">從資源庫新增 Front</span><span class="sxs-lookup"><span data-stu-id="4734a-123">Adding Front from the gallery</span></span>
<span data-ttu-id="4734a-124">若要設定將 Front 整合到 Azure AD 中，您需要從資源庫將 Front 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="4734a-124">To configure the integration of Front into Azure AD, you need to add Front from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4734a-125">**若要從資源庫新增 Front，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4734a-125">**To add Front from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="4734a-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="4734a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="4734a-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4734a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="4734a-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4734a-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="4734a-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="4734a-133">在搜尋方塊中，輸入 **Front**，從結果面板中選取 [Front]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="4734a-133">In the search box, type **Front**, select **Front** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Front](./media/active-directory-saas-front-tutorial/tutorial_front_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4734a-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4734a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4734a-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，設定及測試與 Front 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-136">In this section, you configure and test Azure AD single sign-on with Front based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4734a-137">若要讓單一登入運作，Azure AD 必須知道 Front 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="4734a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Front is to a user in Azure AD.</span></span> <span data-ttu-id="4734a-138">換句話說，必須在 Azure AD 使用者與 Front 中的相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4734a-138">In other words, a link relationship between an Azure AD user and the related user in Front needs to be established.</span></span>

<span data-ttu-id="4734a-139">在 Front 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="4734a-139">In Front, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="4734a-140">若要設定及測試與 Front 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="4734a-140">To configure and test Azure AD single sign-on with Front, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4734a-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="4734a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="4734a-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4734a-143">**[建立 Front 測試使用者](#create-a-front-test-user)** - 在 Front 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="4734a-143">**[Create a Front test user](#create-a-front-test-user)** - to have a counterpart of Britta Simon in Front that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4734a-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4734a-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="4734a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4734a-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="4734a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4734a-147">在本節中，您會於 Azure 入口網站啟用 Azure AD 單一登入，然後在您的 Front 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Front application.</span></span>

<span data-ttu-id="4734a-148">**若要設定與 Front 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4734a-148">**To configure Azure AD single sign-on with Front, perform the following steps:**</span></span>

1. <span data-ttu-id="4734a-149">在 Azure 入口網站的 [Front] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="4734a-149">In the Azure portal, on the **Front** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="4734a-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-front-tutorial/tutorial_front_samlbase.png)

3. <span data-ttu-id="4734a-153">如果您想要以 **IDP** 起始模式設定應用程式，請在 [Front 網域及 URL] 區段上執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4734a-153">On the **Front Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_url1.png)

    <span data-ttu-id="4734a-155">a.</span><span class="sxs-lookup"><span data-stu-id="4734a-155">a.</span></span> <span data-ttu-id="4734a-156">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="4734a-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>

    <span data-ttu-id="4734a-157">b.</span><span class="sxs-lookup"><span data-stu-id="4734a-157">b.</span></span> <span data-ttu-id="4734a-158">在 [回覆 URL] 文字方塊中，以下列模式輸入 URL：`https://<companyname>.frontapp.com/sso/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="4734a-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com/sso/saml/callback`</span></span>

4. <span data-ttu-id="4734a-159">如果您想要以 **SP** 起始模式設定應用程式，請勾選 [顯示進階 URL 設定]：</span><span class="sxs-lookup"><span data-stu-id="4734a-159">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_url2.png)

    <span data-ttu-id="4734a-161">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<companyname>.frontapp.com`</span><span class="sxs-lookup"><span data-stu-id="4734a-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.frontapp.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="4734a-162">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="4734a-162">These values are not real.</span></span> <span data-ttu-id="4734a-163">請使用實際的「識別碼」、「回覆 URL」及「單一登入 URL」更新這些值 (本教學課程稍後會說明)，或連絡 [Front 用戶端支援小組](mailto:support@frontapp.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="4734a-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL which are explained later in tutorial or contact [Front Client support team](mailto:support@frontapp.com) to get these values.</span></span> 

5. <span data-ttu-id="4734a-164">在 [SAML 簽署憑證] 區段上，按一下 [憑證 (Base64)]，然後將憑證檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="4734a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_certificate.png) 

6. <span data-ttu-id="4734a-166">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-166">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="4734a-168">在 [Front 組態] 區段上，按一下 [設定 Front] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4734a-168">On the **Front Configuration** section, click **Configure Front** to open **Configure sign-on** window.</span></span> <span data-ttu-id="4734a-169">從 [快速參考] 區段中複製 [登出 URL、SAML 實體識別碼和 SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="4734a-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_configure.png) 

8. <span data-ttu-id="4734a-171">以系統管理員身分登入 Front 租用戶。</span><span class="sxs-lookup"><span data-stu-id="4734a-171">Sign-on to your Front tenant as an administrator.</span></span>

9. <span data-ttu-id="4734a-172">移至 [設定] \(左側資訊看板底部的齒輪圖示) > [喜好設定]。</span><span class="sxs-lookup"><span data-stu-id="4734a-172">Go to **Settings (cog icon at the bottom of the left sidebar) > Preferences**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_000.png)

10. <span data-ttu-id="4734a-174">按一下 [單一登入]  連結。</span><span class="sxs-lookup"><span data-stu-id="4734a-174">Click **Single Sign On** link.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_001.png)

11. <span data-ttu-id="4734a-176">從 [單一登入] 下拉式清單中選取 [SAML]。</span><span class="sxs-lookup"><span data-stu-id="4734a-176">Select **SAML** in the drop-down list of **Single Sign On**.</span></span>
   
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_002.png)

12. <span data-ttu-id="4734a-178">在 [進入點] 文字方塊中，放入來自 Azure AD 應用程式組態精靈的 [單一登入服務 URL] 值。</span><span class="sxs-lookup"><span data-stu-id="4734a-178">In the **Entry Point** textbox put the value of **Single Sign-on Service URL** from Azure AD application configuration wizard.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_003.png)

13. <span data-ttu-id="4734a-180">在記事本中開啟您下載的**憑證 (Base64)** 檔案，將其內容複製到剪貼簿，然後貼到 [簽署憑證] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="4734a-180">Open your downloaded **Certificate(Base64)** file in notepad, copy the content of it into your clipboard, and then paste it to the **Signing certificate** textbox.</span></span>
    
    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_004.png)

14. <span data-ttu-id="4734a-182">在 [服務提供者設定] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4734a-182">On the **Service provider settings** section, perform the following steps:</span></span>

    ![在應用程式端設定單一登入](./media/active-directory-saas-front-tutorial/tutorial_front_005.png)

    <span data-ttu-id="4734a-184">a.</span><span class="sxs-lookup"><span data-stu-id="4734a-184">a.</span></span> <span data-ttu-id="4734a-185">複製**實體識別碼**值，並在 Azure 入口網站 [Front 網域與 URL] 區段的 [識別碼] 文字方塊中貼上。</span><span class="sxs-lookup"><span data-stu-id="4734a-185">Copy the value of **Entity ID** and paste it into the **Identifier** textbox in **Front Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="4734a-186">b.</span><span class="sxs-lookup"><span data-stu-id="4734a-186">b.</span></span> <span data-ttu-id="4734a-187">複製**ACS URL**值，並在 Azure 入口網站 [Front 網域與 URL] 區段的 [單一登入 URL] 文字方塊中貼上。</span><span class="sxs-lookup"><span data-stu-id="4734a-187">Copy the value of **ACS URL** and paste it into the **Sign-on URL** textbox in **Front Domain and URLs** section in Azure portal.</span></span>
    
15. <span data-ttu-id="4734a-188">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-188">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="4734a-189">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="4734a-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4734a-190">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="4734a-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4734a-191">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4734a-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4734a-192">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4734a-192">Create an Azure AD test user</span></span>

<span data-ttu-id="4734a-193">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="4734a-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="4734a-195">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4734a-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="4734a-196">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-196">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-front-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4734a-198">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="4734a-198">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-front-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4734a-200">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="4734a-200">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-front-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4734a-202">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4734a-202">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-front-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4734a-204">a.</span><span class="sxs-lookup"><span data-stu-id="4734a-204">a.</span></span> <span data-ttu-id="4734a-205">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="4734a-205">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4734a-206">b.</span><span class="sxs-lookup"><span data-stu-id="4734a-206">b.</span></span> <span data-ttu-id="4734a-207">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="4734a-207">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="4734a-208">c.</span><span class="sxs-lookup"><span data-stu-id="4734a-208">c.</span></span> <span data-ttu-id="4734a-209">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="4734a-209">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="4734a-210">d.</span><span class="sxs-lookup"><span data-stu-id="4734a-210">d.</span></span> <span data-ttu-id="4734a-211">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="4734a-211">Click **Create**.</span></span>
 
### <a name="create-a-front-test-user"></a><span data-ttu-id="4734a-212">建立 Front 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4734a-212">Create a Front test user</span></span>

<span data-ttu-id="4734a-213">在本節中，您會於 Front 建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="4734a-213">In this section, you create a user called Britta Simon in Front.</span></span> <span data-ttu-id="4734a-214">請與 [Front 客戶支援小組](mailto:support@frontapp.com)合作，在 Front 平台中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="4734a-214">Work with [Front Client support team](mailto:support@frontapp.com) to add the users in the Front platform.</span></span> <span data-ttu-id="4734a-215">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-215">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4734a-216">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="4734a-216">Assign the Azure AD test user</span></span>

<span data-ttu-id="4734a-217">在本節中，您會將 Front 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="4734a-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Front.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="4734a-219">**若要將 Britta Simon 指派給 Front，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="4734a-219">**To assign Britta Simon to Front, perform the following steps:**</span></span>

1. <span data-ttu-id="4734a-220">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="4734a-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="4734a-222">在應用程式清單中，選取 [Fuse] 。</span><span class="sxs-lookup"><span data-stu-id="4734a-222">In the applications list, select **Front**.</span></span>

    ![應用程式清單中的 Front 連結](./media/active-directory-saas-front-tutorial/tutorial_front_app.png)  

3. <span data-ttu-id="4734a-224">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4734a-224">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="4734a-226">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-226">Click **Add** button.</span></span> <span data-ttu-id="4734a-227">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="4734a-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="4734a-229">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="4734a-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="4734a-230">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4734a-231">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4734a-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4734a-232">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="4734a-232">Test single sign-on</span></span>

<span data-ttu-id="4734a-233">本節的目標是要使用存取面板來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="4734a-233">The objective of this section is to test your Azure AD SSOconfiguration using the Access Panel.</span></span>

<span data-ttu-id="4734a-234">當您在「存取面板」中按一下 [Front] 磚時，應該會自動登入您的 Front 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4734a-234">When you click the Front tile in the Access Panel, you should get automatically signed-on to your Front application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4734a-235">其他資源</span><span class="sxs-lookup"><span data-stu-id="4734a-235">Additional resources</span></span>

* [<span data-ttu-id="4734a-236">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="4734a-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4734a-237">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="4734a-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-front-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-front-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-front-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-front-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-front-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-front-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-front-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-front-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-front-tutorial/tutorial_general_203.png

