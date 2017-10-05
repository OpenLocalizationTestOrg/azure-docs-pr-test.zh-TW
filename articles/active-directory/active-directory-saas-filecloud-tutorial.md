---
title: "教學課程：Azure Active Directory 與 FileCloud 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 FileCloud 間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ad03516f684acc59912ffc57f6e0712828bd03f2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="6c7c5-103">教學課程：Azure Active Directory 與 FileCloud 整合</span><span class="sxs-lookup"><span data-stu-id="6c7c5-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="6c7c5-104">在本教學課程中，您會了解如何整合 FileCloud 與 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-104">In this tutorial, you learn how to integrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c7c5-105">FileCloud 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-105">Integrating FileCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c7c5-106">您可以在 Azure AD 中控制可存取 FileCloud 的人員。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-106">You can control in Azure AD who has access to FileCloud.</span></span>
- <span data-ttu-id="6c7c5-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 FileCloud (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-107">You can enable your users to automatically get signed-on to FileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6c7c5-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="6c7c5-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c7c5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="6c7c5-110">Prerequisites</span></span>

<span data-ttu-id="6c7c5-111">若要設定 Azure AD 與 FileCloud 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-111">To configure Azure AD integration with FileCloud, you need the following items:</span></span>

- <span data-ttu-id="6c7c5-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6c7c5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c7c5-113">已啟用 FileCloud 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6c7c5-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c7c5-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c7c5-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c7c5-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c7c5-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c7c5-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="6c7c5-118">Scenario description</span></span>
<span data-ttu-id="6c7c5-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c7c5-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c7c5-121">從資源庫新增 FileCloud</span><span class="sxs-lookup"><span data-stu-id="6c7c5-121">Adding FileCloud from the gallery</span></span>
2. <span data-ttu-id="6c7c5-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c7c5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-the-gallery"></a><span data-ttu-id="6c7c5-123">從資源庫新增 FileCloud</span><span class="sxs-lookup"><span data-stu-id="6c7c5-123">Adding FileCloud from the gallery</span></span>
<span data-ttu-id="6c7c5-124">若要設定將 FileCloud 整合到 Azure AD 中，您需要從資源庫將 FileCloud 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-124">To configure the integration of FileCloud into Azure AD, you need to add FileCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c7c5-125">**若要從資源庫新增 FileCloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c7c5-125">**To add FileCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c5-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="6c7c5-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c7c5-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="6c7c5-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="6c7c5-133">在搜尋方塊中，輸入 **FileCloud**，從結果面板中選取 **FileCloud**，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-133">In the search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6c7c5-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c7c5-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6c7c5-136">在本節中，您會以名為 "Britta Simon" 的測試使用者身分，使用 FileCloud 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c7c5-137">若要讓單一登入能夠運作，Azure AD 必須知道 FileCloud 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-137">For single sign-on to work, Azure AD needs to know what the counterpart user in FileCloud is to a user in Azure AD.</span></span> <span data-ttu-id="6c7c5-138">換句話說，必須建立 Azure AD 使用者和 FileCloud 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-138">In other words, a link relationship between an Azure AD user and the related user in FileCloud needs to be established.</span></span>

<span data-ttu-id="6c7c5-139">在 FileCloud 中，將 Azure AD 中 [使用者名稱] 的值指派為 [使用者名稱] 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-139">In FileCloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6c7c5-140">若要使用 FileCloud 設定及測試 Azure AD 單一登入功能，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-140">To configure and test Azure AD single sign-on with FileCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c7c5-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6c7c5-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c7c5-143">**[建立 FileCloud 測試使用者](#create-a-filecloud-test-user)** - 在 FileCloud 中建立 Britta Simon 的對應項目，且該項目與 Azure AD 中代表使用者的項目連結。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - to have a counterpart of Britta Simon in FileCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c7c5-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c7c5-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6c7c5-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="6c7c5-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6c7c5-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 FileCloud 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="6c7c5-148">**若要使用 FileCloud 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c7c5-148">**To configure Azure AD single sign-on with FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c5-149">在 Azure 入口網站的 [FileCloud] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-149">In the Azure portal, on the **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="6c7c5-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="6c7c5-153">在 [FileCloud 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-153">On the **FileCloud Domain and URLs** section, perform the following steps:</span></span>

    ![FileCloud 網域和 URL 單一登入資訊](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="6c7c5-155">a.</span><span class="sxs-lookup"><span data-stu-id="6c7c5-155">a.</span></span> <span data-ttu-id="6c7c5-156">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="6c7c5-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="6c7c5-157">b.</span><span class="sxs-lookup"><span data-stu-id="6c7c5-157">b.</span></span> <span data-ttu-id="6c7c5-158">在 [識別碼] 文字方塊中，使用下列模式輸入 URL：`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="6c7c5-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6c7c5-159">這些都不是真正的值。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-159">These values are not real.</span></span> <span data-ttu-id="6c7c5-160">使用實際的「登入 URL」及「識別碼」來更新這些值。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6c7c5-161">請連絡 [FileCloud 用戶端支援小組](mailto:support@codelathe.com)以取得這些值。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) to get these values.</span></span>

4. <span data-ttu-id="6c7c5-162">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="6c7c5-164">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-164">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c7c5-166">在 [FileCloud 設定] 區段上，按一下 [設定 FileCloud] 可開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-166">On the **FileCloud Configuration** section, click **Configure FileCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6c7c5-167">從 [快速參考] 區段中複製 [SAML 實體識別碼]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-167">Copy the **SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![FileCloud 設定](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="6c7c5-169">在不同的網頁瀏覽器視窗中，以管理員身分登入您的 FileCloud 租用戶。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-169">In a different web browser window, sign-on to your FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="6c7c5-170">在左側的導覽窗格上，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-170">On the left navigation pane, click **Settings**.</span></span> 
   
    ![應用程式端上的設定區段](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="6c7c5-172">按一下 [設定] 區段上的 [SSO] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![應用程式端上的單一登入索引標籤](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="6c7c5-174">在 **Single Sign On (SSO) Settings** (單一登入 (SSO) 設定) 面板上，選取 **SAML** 作為 **Default SSO Type** (預設 SSO 類型)。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![應用程式端上的單一登入設定面板](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="6c7c5-176">將您從 Azure 入口網站複製的「SAML 實體識別碼」貼到 [IdP 端點 URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-176">Paste **SAML Entity ID**, which you have copied from Azure portal into the **IdP End Point URL** textbox.</span></span>

    ![IDP 端點 URL 文字方塊](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="6c7c5-178">在記事本中開啟您下載的中繼資料，將其內容複製到剪貼簿上，然後貼到 **SAML Settings** (SAML 設定) 面板的 **IdP Meta Data** (IdP 中繼資料) 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-178">Open your downloaded metadata file in notepad, copy the content of it into your clipboard, and then paste it to the **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![應用程式端上的 IDP 中繼資料區段](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="6c7c5-180">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="6c7c5-181">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="6c7c5-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6c7c5-182">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6c7c5-183">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c7c5-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6c7c5-184">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c7c5-184">Create an Azure AD test user</span></span>

<span data-ttu-id="6c7c5-185">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="6c7c5-187">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c7c5-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c5-188">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-188">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6c7c5-190">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-190">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6c7c5-192">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-192">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6c7c5-194">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6c7c5-194">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="6c7c5-196">a.</span><span class="sxs-lookup"><span data-stu-id="6c7c5-196">a.</span></span> <span data-ttu-id="6c7c5-197">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-197">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c7c5-198">b.</span><span class="sxs-lookup"><span data-stu-id="6c7c5-198">b.</span></span> <span data-ttu-id="6c7c5-199">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-199">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="6c7c5-200">c.</span><span class="sxs-lookup"><span data-stu-id="6c7c5-200">c.</span></span> <span data-ttu-id="6c7c5-201">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-201">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="6c7c5-202">d.</span><span class="sxs-lookup"><span data-stu-id="6c7c5-202">d.</span></span> <span data-ttu-id="6c7c5-203">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="6c7c5-204">建立 FileCloud 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c7c5-204">Create a FileCloud test user</span></span>

<span data-ttu-id="6c7c5-205">本節的目標是要在 FileCloud 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-205">The objective of this section is to create a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="6c7c5-206">FileCloud 支援預設啟用的 Just-In-Time 佈建。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="6c7c5-207">在這一節沒有您需要進行的動作項目。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-207">There is no action item for you in this section.</span></span> <span data-ttu-id="6c7c5-208">嘗試存取 FileCloud 時，如果使用者尚未存在，就會建立新使用者。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-208">A new user is created during an attempt to access FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="6c7c5-209">如果您需要手動建立使用者，您需要連絡 [FileCloud 用戶端支援小組](mailto:support@codelathe.com)。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-209">If you need to create a user manually, you need to contact the [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="6c7c5-210">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="6c7c5-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="6c7c5-211">在本節中，您會將 FileCloud 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FileCloud.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="6c7c5-213">**若要將 Britta Simon 指派給 FileCloud，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="6c7c5-213">**To assign Britta Simon to FileCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="6c7c5-214">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="6c7c5-216">在應用程式清單中，選取 [FileCloud] 。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-216">In the applications list, select **FileCloud**.</span></span>

    ![應用程式清單中的 FileCloud 連結](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="6c7c5-218">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-218">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="6c7c5-220">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-220">Click **Add** button.</span></span> <span data-ttu-id="6c7c5-221">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="6c7c5-223">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6c7c5-224">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c7c5-225">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6c7c5-226">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="6c7c5-226">Test single sign-on</span></span>

<span data-ttu-id="6c7c5-227">本節的目標是要使用「存取面板」來測試您的 Azure AD SSO 組態。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="6c7c5-228">當您在存取面板中按一下 [FileCloud] 圖格時，應該會自動登入您的 FileCloud 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c7c5-228">When you click the FileCloud tile in the Access Panel, you should get automatically signed-on to your FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6c7c5-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="6c7c5-229">Additional resources</span></span>

* [<span data-ttu-id="6c7c5-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="6c7c5-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c7c5-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="6c7c5-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

