---
title: "教學課程：Azure Active Directory 與 ArcGIS Online 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 ArcGIS Online 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: df72270ca6443b456c079b22425f1660aa522389
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="ce796-103">教學課程：Azure Active Directory 與 ArcGIS Online 整合</span><span class="sxs-lookup"><span data-stu-id="ce796-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="ce796-104">在本教學課程中，您會了解如何將 ArcGIS Online 與 Azure Active Directory (Azure AD) 整合。</span><span class="sxs-lookup"><span data-stu-id="ce796-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ce796-105">將 ArcGIS Online 與 Azure AD 整合可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="ce796-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ce796-106">您可以在 Azure AD 中控制可存取 ArcGIS Online 的人員</span><span class="sxs-lookup"><span data-stu-id="ce796-106">You can control in Azure AD who has access to ArcGIS Online</span></span>
- <span data-ttu-id="ce796-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 ArcGIS Online (單一登入)</span><span class="sxs-lookup"><span data-stu-id="ce796-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ce796-108">您可以在 Azure 入口網站中集中管理您的帳戶</span><span class="sxs-lookup"><span data-stu-id="ce796-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ce796-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="ce796-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

To enable single sign-on with ArcGIS Online, it must be configured to use Azure Active Directory as an identity provider. This guide provides information and tips on how to perform this configuration in ArcGIS Online.

>[!Note]: 
>This embedded guide is brand new in the new Azure portal, and we’d love to hear your thoughts. Use the Feedback ? button at the top of the portal to provide feedback. The older guide for using the [Azure classic portal](https://manage.windowsazure.com) to configure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="ce796-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ce796-110">Prerequisites</span></span>

<span data-ttu-id="ce796-111">若要設定 Azure AD 與 ArcGIS Online 的整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ce796-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="ce796-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ce796-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ce796-113">已啟用 ArcGIS Online 單一登入功能的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ce796-113">A ArcGIS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ce796-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ce796-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ce796-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="ce796-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ce796-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="ce796-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ce796-117">如果您沒有 Azure AD 試用環境，您可以在 [這裡](https://azure.microsoft.com/pricing/free-trial/)取得一個月試用。</span><span class="sxs-lookup"><span data-stu-id="ce796-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ce796-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="ce796-118">Scenario description</span></span>
<span data-ttu-id="ce796-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ce796-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="ce796-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ce796-121">從資源庫新增 ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="ce796-121">Adding ArcGIS Online from the gallery</span></span>
2. <span data-ttu-id="ce796-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ce796-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="ce796-123">從資源庫新增 ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="ce796-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="ce796-124">若要設定將 ArcGIS Online 整合到 Azure AD 中，您需要從資源庫將 ArcGIS Online 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="ce796-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ce796-125">**若要從資源庫新增 ArcGIS Online，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ce796-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ce796-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ce796-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ce796-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ce796-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ce796-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ce796-129">Then go to **All applications**.</span></span>

    ![應用程式][2]
    
3. <span data-ttu-id="ce796-131">按一下對話方塊頂端的 [新應用程式] 按鈕來新增新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce796-131">Click **New application** button on the top of the dialog to add new application.</span></span>

    ![應用程式][3]

4. <span data-ttu-id="ce796-133">在搜尋方塊中，輸入 **ArcGIS Online**。</span><span class="sxs-lookup"><span data-stu-id="ce796-133">In the search box, type **ArcGIS Online**.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_search.png)

5. <span data-ttu-id="ce796-135">在結果面板中，選取 [ArcGIS Online]，然後按一下 [新增] 按鈕以新增該應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce796-135">In the results panel, select **ArcGIS Online**, and then click **Add** button to add the application.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ce796-137">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ce796-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ce796-138">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 ArcGIS Online 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-138">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ce796-139">若要讓單一登入能夠運作，Azure AD 必須知道 ArcGIS Online 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="ce796-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="ce796-140">換句話說，必須在 Azure AD 使用者與 ArcGIS Online 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="ce796-140">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="ce796-141">建立此連結關聯性的方法，就是將 ArcGIS Online 中 [使用者名稱] 的值指派為 Azure AD 中 [使用者名稱] 的值。</span><span class="sxs-lookup"><span data-stu-id="ce796-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ArcGIS Online.</span></span>

<span data-ttu-id="ce796-142">若要設定及測試與 ArcGIS Online 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="ce796-142">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ce796-143">**[設定 Azure AD 單一登入](#configuring-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="ce796-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ce796-144">**[建立 Azure AD 測試使用者](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ce796-145">**[建立 ArcGIS Online 測試使用者](#creating-an-arcgis-online-test-user)** - 在 ArcGIS Online 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="ce796-145">**[Creating an ArcGIS Online test user](#creating-an-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ce796-146">**[指派 Azure AD 測試使用者](#assigning-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ce796-147">**[Testing Single Sign-On](#testing-single-sign-on)** - 驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="ce796-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ce796-148">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="ce796-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ce796-149">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 ArcGIS Online 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="ce796-150">**若要設定與 ArcGIS Online 搭配運作的 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ce796-150">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="ce796-151">在 Azure 入口網站的 [ArcGIS Online] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="ce796-151">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入][4]

2. <span data-ttu-id="ce796-153">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

3. <span data-ttu-id="ce796-155">在 [ArcGIS Online 網域及 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ce796-155">On the **ArcGIS Online Domain and URLs** section, perform the following step:</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="ce796-157">在 [登入 URL] 文字方塊中，以下列模式輸入值：`https://<company>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="ce796-157">In the **Sign-on URL** textbox, type the value using the following pattern: `https://<company>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ce796-158">這不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="ce796-158">This value is not the real.</span></span> <span data-ttu-id="ce796-159">使用實際的「登入 URL」來更新此值。</span><span class="sxs-lookup"><span data-stu-id="ce796-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ce796-160">請連絡 [ArcGIS Online 用戶端支援小組](http://support.esri.com/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="ce796-160">Contact [ArcGIS Online Client support team](http://support.esri.com/) to get this value.</span></span> 

4. <span data-ttu-id="ce796-161">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將 XML 檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="ce796-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

5. <span data-ttu-id="ce796-163">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce796-163">Click **Save** button.</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ce796-165">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 ArcGIS 公司網站。</span><span class="sxs-lookup"><span data-stu-id="ce796-165">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

7. <span data-ttu-id="ce796-166">按一下 [編輯設定]。</span><span class="sxs-lookup"><span data-stu-id="ce796-166">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="ce796-167">![編輯設定](./media/active-directory-saas-arcgis-tutorial/ic784742.png "編輯設定")</span><span class="sxs-lookup"><span data-stu-id="ce796-167">![Edit Settings](./media/active-directory-saas-arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

8. <span data-ttu-id="ce796-168">按一下 [安全性] 。</span><span class="sxs-lookup"><span data-stu-id="ce796-168">Click **Security**.</span></span>

    <span data-ttu-id="ce796-169">![安全性](./media/active-directory-saas-arcgis-tutorial/ic784743.png "安全性")</span><span class="sxs-lookup"><span data-stu-id="ce796-169">![Security](./media/active-directory-saas-arcgis-tutorial/ic784743.png "Security")</span></span>

9. <span data-ttu-id="ce796-170">在 [企業登入] 下方，按一下 [設定識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="ce796-170">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="ce796-171">![企業登入](./media/active-directory-saas-arcgis-tutorial/ic784744.png "企業登入")</span><span class="sxs-lookup"><span data-stu-id="ce796-171">![Enterprise Logins](./media/active-directory-saas-arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

10. <span data-ttu-id="ce796-172">在 [設定識別提供者]  組態頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ce796-172">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="ce796-173">![設定識別提供者](./media/active-directory-saas-arcgis-tutorial/ic784745.png "設定識別提供者")</span><span class="sxs-lookup"><span data-stu-id="ce796-173">![Set Identity Provider](./media/active-directory-saas-arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="ce796-174">a.</span><span class="sxs-lookup"><span data-stu-id="ce796-174">a.</span></span> <span data-ttu-id="ce796-175">在 [名稱] 文字方塊中，輸入您的組織名稱。</span><span class="sxs-lookup"><span data-stu-id="ce796-175">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="ce796-176">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce796-176">b.</span></span> <span data-ttu-id="ce796-177">針對 [用來提供企業識別提供者之中繼資料的方法]，選取 [檔案]。</span><span class="sxs-lookup"><span data-stu-id="ce796-177">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="ce796-178">c.</span><span class="sxs-lookup"><span data-stu-id="ce796-178">c.</span></span> <span data-ttu-id="ce796-179">若要上傳您下載的中繼資料檔，請按一下 [選擇檔案] 。</span><span class="sxs-lookup"><span data-stu-id="ce796-179">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="ce796-180">d.</span><span class="sxs-lookup"><span data-stu-id="ce796-180">d.</span></span> <span data-ttu-id="ce796-181">按一下 [設定識別提供者]。</span><span class="sxs-lookup"><span data-stu-id="ce796-181">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="ce796-182">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="ce796-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ce796-183">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="ce796-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ce796-184">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ce796-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ce796-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ce796-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="ce796-186">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="ce796-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![建立 Azure AD 使用者][100]

<span data-ttu-id="ce796-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ce796-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ce796-189">在 **Azure 入口網站**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="ce796-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ce796-191">移至 [使用者和群組]，然後按一下 [所有使用者] 以顯示使用者清單。</span><span class="sxs-lookup"><span data-stu-id="ce796-191">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ce796-193">在對話方塊的頂端，按一下 [新增] 以開啟 [使用者] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="ce796-193">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ce796-195">在 [使用者]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ce796-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![建立 Azure AD 測試使用者](./media/active-directory-saas-arcgis-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ce796-197">a.</span><span class="sxs-lookup"><span data-stu-id="ce796-197">a.</span></span> <span data-ttu-id="ce796-198">在 [名稱] 文字方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="ce796-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ce796-199">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce796-199">b.</span></span> <span data-ttu-id="ce796-200">在 [使用者名稱] 文字方塊中，輸入 Britta Simon 的「電子郵件地址」。</span><span class="sxs-lookup"><span data-stu-id="ce796-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="ce796-201">c.</span><span class="sxs-lookup"><span data-stu-id="ce796-201">c.</span></span> <span data-ttu-id="ce796-202">選取 [顯示密碼] 並記下 [密碼] 的值。</span><span class="sxs-lookup"><span data-stu-id="ce796-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ce796-203">d.</span><span class="sxs-lookup"><span data-stu-id="ce796-203">d.</span></span> <span data-ttu-id="ce796-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="ce796-204">Click **Create**.</span></span>
 
### <a name="creating-an-arcgis-online-test-user"></a><span data-ttu-id="ce796-205">建立 ArcGIS Online 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ce796-205">Creating an ArcGIS Online test user</span></span>

<span data-ttu-id="ce796-206">若要讓 Azure AD 使用者能夠登入 ArcGIS Online，必須將他們佈建到 ArcGIS Online。</span><span class="sxs-lookup"><span data-stu-id="ce796-206">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="ce796-207">就 ArcGIS Online 而言，需以手動方式佈建。</span><span class="sxs-lookup"><span data-stu-id="ce796-207">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="ce796-208">**若要佈建使用者帳戶，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ce796-208">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ce796-209">登入您的 **ArcGIS** 租用戶。</span><span class="sxs-lookup"><span data-stu-id="ce796-209">Log in to your **ArcGIS** tenant.</span></span>

2. <span data-ttu-id="ce796-210">按一下 [邀請成員]。</span><span class="sxs-lookup"><span data-stu-id="ce796-210">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="ce796-211">![邀請成員](./media/active-directory-saas-arcgis-tutorial/ic784747.png "邀請成員")</span><span class="sxs-lookup"><span data-stu-id="ce796-211">![Invite Members](./media/active-directory-saas-arcgis-tutorial/ic784747.png "Invite Members")</span></span>

3. <span data-ttu-id="ce796-212">選取 [自動新增成員而不傳送電子郵件]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="ce796-212">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="ce796-213">![自動新增成員](./media/active-directory-saas-arcgis-tutorial/ic784748.png "自動新增成員")</span><span class="sxs-lookup"><span data-stu-id="ce796-213">![Add Members Automatically](./media/active-directory-saas-arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

4. <span data-ttu-id="ce796-214">在 [成員]  對話頁面上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="ce796-214">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="ce796-215">![新增並檢閱](./media/active-directory-saas-arcgis-tutorial/ic784749.png "新增並檢閱")</span><span class="sxs-lookup"><span data-stu-id="ce796-215">![Add and review](./media/active-directory-saas-arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="ce796-216">a.</span><span class="sxs-lookup"><span data-stu-id="ce796-216">a.</span></span> <span data-ttu-id="ce796-217">輸入您想要佈建之有效 AAD 帳戶的 [電子郵件]、[名字] 和 [姓氏]。</span><span class="sxs-lookup"><span data-stu-id="ce796-217">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="ce796-218">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce796-218">b.</span></span> <span data-ttu-id="ce796-219">按一下 [新增並檢閱]。</span><span class="sxs-lookup"><span data-stu-id="ce796-219">Click **ADD AND REVIEW**.</span></span>
5. <span data-ttu-id="ce796-220">檢閱您已輸入的資料，然後按一下 [新增成員]。</span><span class="sxs-lookup"><span data-stu-id="ce796-220">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="ce796-221">![新增成員](./media/active-directory-saas-arcgis-tutorial/ic784750.png "新增成員")</span><span class="sxs-lookup"><span data-stu-id="ce796-221">![Add member](./media/active-directory-saas-arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="ce796-222">Azure Active Directory 帳戶的持有者會收到一封電子郵件，並依照連結在啟用其帳戶前進行確認。</span><span class="sxs-lookup"><span data-stu-id="ce796-222">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ce796-223">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="ce796-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ce796-224">在本節中，您會將 ArcGIS Online 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="ce796-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![指派使用者][200] 

<span data-ttu-id="ce796-226">**若要將 Britta Simon 指派給 ArcGIS Online，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="ce796-226">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="ce796-227">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="ce796-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="ce796-229">在應用程式清單中，選取 [ArcGIS Online]。</span><span class="sxs-lookup"><span data-stu-id="ce796-229">In the applications list, select **ArcGIS Online**.</span></span>

    ![設定單一登入](./media/active-directory-saas-arcgis-tutorial/tutorial_arcgisonline_app.png) 

3. <span data-ttu-id="ce796-231">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ce796-231">In the menu on the left, click **Users and groups**.</span></span>

    ![指派使用者][202] 

4. <span data-ttu-id="ce796-233">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce796-233">Click **Add** button.</span></span> <span data-ttu-id="ce796-234">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="ce796-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![指派使用者][203]

5. <span data-ttu-id="ce796-236">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="ce796-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ce796-237">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce796-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ce796-238">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ce796-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ce796-239">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="ce796-239">Testing single sign-on</span></span>

<span data-ttu-id="ce796-240">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="ce796-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ce796-241">當您在「存取面板」中按一下 [ArcGIS Online] 圖格時，應該會自動登入您的 ArcGIS Online 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ce796-241">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="ce796-242">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="ce796-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ce796-243">其他資源</span><span class="sxs-lookup"><span data-stu-id="ce796-243">Additional resources</span></span>

* [<span data-ttu-id="ce796-244">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="ce796-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ce796-245">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="ce796-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-arcgis-tutorial/tutorial_general_203.png

