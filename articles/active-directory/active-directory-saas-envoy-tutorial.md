---
title: "教學課程：Azure Active Directory 與 Envoy 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Envoy 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="7bea1-103">教學課程：Azure Active Directory 與 Envoy 整合</span><span class="sxs-lookup"><span data-stu-id="7bea1-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="7bea1-104">在本教學課程中，您會了解如何將 Envoy 與 Azure Active Directory (Azure AD) 進行整合。</span><span class="sxs-lookup"><span data-stu-id="7bea1-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7bea1-105">Envoy 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="7bea1-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7bea1-106">您可以在 Azure AD 中控制可存取 Envoy 的人員。</span><span class="sxs-lookup"><span data-stu-id="7bea1-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="7bea1-107">您可以讓使用者使用他們的 Azure AD 帳戶自動登入 Envoy (單一登入)。</span><span class="sxs-lookup"><span data-stu-id="7bea1-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7bea1-108">您可以在 Azure 入口網站中集中管理您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7bea1-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="7bea1-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="7bea1-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bea1-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="7bea1-110">Prerequisites</span></span>

<span data-ttu-id="7bea1-111">若要設定 Azure AD 與 Envoy 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="7bea1-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="7bea1-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7bea1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7bea1-113">啟用 Envoy 單一登入的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="7bea1-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7bea1-114">若要測試本教學課程中的步驟，我們不建議使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7bea1-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7bea1-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="7bea1-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7bea1-116">除非必要，否則請勿使用生產環境。</span><span class="sxs-lookup"><span data-stu-id="7bea1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7bea1-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="7bea1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7bea1-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="7bea1-118">Scenario description</span></span>
<span data-ttu-id="7bea1-119">在本教學課程中，您會在測試環境中測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7bea1-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="7bea1-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7bea1-121">從資源庫新增 Envoy</span><span class="sxs-lookup"><span data-stu-id="7bea1-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="7bea1-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7bea1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="7bea1-123">從資源庫新增 Envoy</span><span class="sxs-lookup"><span data-stu-id="7bea1-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="7bea1-124">若要設定將 Envoy 整合到 Azure AD 中，您需要從資源庫將 Envoy 新增到受管理的 SaaS 應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="7bea1-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7bea1-125">**若要從資源庫新增 Envoy，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7bea1-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7bea1-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="7bea1-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="7bea1-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7bea1-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="7bea1-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7bea1-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="7bea1-133">在搜尋方塊中，輸入 **Envoy**，從結果面板中選取 [Envoy]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="7bea1-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7bea1-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7bea1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7bea1-136">在本節中，您會以名為 "Britta Simon" 的測試使用者作為基礎，使用 Envoy 設定及測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7bea1-137">若要讓單一登入運作，Azure AD 必須知道 Envoy 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="7bea1-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="7bea1-138">換句話說，必須建立 Azure AD 使用者和 Envoy 中相關使用者之間的連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7bea1-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="7bea1-139">在 Envoy 中，將 Azure AD 中**使用者名稱**的值指派為 **Username** 的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="7bea1-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7bea1-140">若要設定及測試與 Envoy 搭配運作的 Azure AD 單一登入，您需要完成下列構成要素：</span><span class="sxs-lookup"><span data-stu-id="7bea1-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7bea1-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="7bea1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7bea1-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7bea1-143">**[建立 Envoy 測試使用者](#create-an-envoy-test-user)** - 在 Envoy 中建立一個與 Azure AD 中代表 Britta Simon 之項目連結的 Britta Simon 對應項目。</span><span class="sxs-lookup"><span data-stu-id="7bea1-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7bea1-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7bea1-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="7bea1-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7bea1-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="7bea1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7bea1-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Envoy 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="7bea1-148">**若要使用 Envoy 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7bea1-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="7bea1-149">在 Azure 入口網站的 [Envoy] 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="7bea1-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="7bea1-153">在 [Envoy 網域與 URL] 區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7bea1-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Envoy 網域與 URL 單一登入資訊](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="7bea1-155">在 [登入 URL] 文字方塊中，使用下列模式輸入 URL︰`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="7bea1-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="7bea1-156">這不是真實的值。</span><span class="sxs-lookup"><span data-stu-id="7bea1-156">This value is not real.</span></span> <span data-ttu-id="7bea1-157">請使用實際的登入 URL 來更新此值。</span><span class="sxs-lookup"><span data-stu-id="7bea1-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="7bea1-158">請連絡 [Envoy 用戶端支援小組](https://envoy.com/contact/)以取得此值。</span><span class="sxs-lookup"><span data-stu-id="7bea1-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="7bea1-159">在 [SAML 簽署憑證] 區段上，複製憑證的 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="7bea1-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![憑證下載連結](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="7bea1-161">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="7bea1-161">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7bea1-163">在 [Envoy 組態] 區段上，按一下 [設定 Envoy] 以開啟 [設定登入] 視窗。</span><span class="sxs-lookup"><span data-stu-id="7bea1-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7bea1-164">從 [快速參考] 區段中複製 [SAML 單一登入服務 URL]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Envoy 組態](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="7bea1-166">在不同的網頁瀏覽器視窗中，以系統管理員身分登入您的 Envoy 公司網站。</span><span class="sxs-lookup"><span data-stu-id="7bea1-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="7bea1-167">在頂端的工具列中，按一下 [設定] 。</span><span class="sxs-lookup"><span data-stu-id="7bea1-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="7bea1-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="7bea1-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="7bea1-169">按一下 [公司] 。</span><span class="sxs-lookup"><span data-stu-id="7bea1-169">Click **Company**.</span></span>

    <span data-ttu-id="7bea1-170">![公司](./media/active-directory-saas-envoy-tutorial/ic776783.png "公司")</span><span class="sxs-lookup"><span data-stu-id="7bea1-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="7bea1-171">按一下 [SAML] 。</span><span class="sxs-lookup"><span data-stu-id="7bea1-171">Click **SAML**.</span></span>

    <span data-ttu-id="7bea1-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="7bea1-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="7bea1-173">在 [SAML 驗證]  組態區段中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7bea1-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="7bea1-174">![SAML 驗證](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML 驗證")</span><span class="sxs-lookup"><span data-stu-id="7bea1-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="7bea1-175">總部位置識別碼的值是由應用程式自動產生。</span><span class="sxs-lookup"><span data-stu-id="7bea1-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="7bea1-176">a.</span><span class="sxs-lookup"><span data-stu-id="7bea1-176">a.</span></span> <span data-ttu-id="7bea1-177">在 [指紋] 文字方塊中，貼上您從 Azure 入口網站複製的憑證 [指紋] 值。</span><span class="sxs-lookup"><span data-stu-id="7bea1-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7bea1-178">b.</span><span class="sxs-lookup"><span data-stu-id="7bea1-178">b.</span></span> <span data-ttu-id="7bea1-179">將您從 Azure 入口網站複製的 [SAML 單一登入服務 URL] 值，貼到 [識別提供者 HTTP SAML URL] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="7bea1-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="7bea1-180">c.</span><span class="sxs-lookup"><span data-stu-id="7bea1-180">c.</span></span> <span data-ttu-id="7bea1-181">按一下 [儲存變更] 。</span><span class="sxs-lookup"><span data-stu-id="7bea1-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7bea1-182">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="7bea1-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7bea1-183">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="7bea1-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7bea1-184">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7bea1-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7bea1-185">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7bea1-185">Create an Azure AD test user</span></span>

<span data-ttu-id="7bea1-186">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="7bea1-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="7bea1-188">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7bea1-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7bea1-189">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7bea1-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7bea1-191">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7bea1-193">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7bea1-195">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7bea1-195">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7bea1-197">a.</span><span class="sxs-lookup"><span data-stu-id="7bea1-197">a.</span></span> <span data-ttu-id="7bea1-198">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="7bea1-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7bea1-199">b.</span><span class="sxs-lookup"><span data-stu-id="7bea1-199">b.</span></span> <span data-ttu-id="7bea1-200">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="7bea1-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="7bea1-201">c.</span><span class="sxs-lookup"><span data-stu-id="7bea1-201">c.</span></span> <span data-ttu-id="7bea1-202">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="7bea1-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="7bea1-203">d.</span><span class="sxs-lookup"><span data-stu-id="7bea1-203">d.</span></span> <span data-ttu-id="7bea1-204">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="7bea1-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="7bea1-205">建立 Envoy 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7bea1-205">Create an Envoy test user</span></span>

<span data-ttu-id="7bea1-206">沒有動作項目可讓您設定 Envoy 使用者佈建。</span><span class="sxs-lookup"><span data-stu-id="7bea1-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="7bea1-207">當指派的使用者透過存取面板嘗試登入 Envoy 時，Envoy 會檢查使用者是否存在。</span><span class="sxs-lookup"><span data-stu-id="7bea1-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="7bea1-208">如果尚無可用的使用者帳戶，Envoy 會自動予以建立。</span><span class="sxs-lookup"><span data-stu-id="7bea1-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="7bea1-209">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="7bea1-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="7bea1-210">在本節中，您會將 Envoy 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="7bea1-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![指派使用者角色][200] 

<span data-ttu-id="7bea1-212">**若要將 Britta Simon 指派給 Envoy，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="7bea1-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="7bea1-213">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="7bea1-215">在應用程式清單中，選取 [Envoy]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-215">In the applications list, select **Envoy**.</span></span>

    ![應用程式清單中的 Envoy 連結](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="7bea1-217">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-217">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="7bea1-219">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7bea1-219">Click **Add** button.</span></span> <span data-ttu-id="7bea1-220">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="7bea1-222">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="7bea1-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7bea1-223">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7bea1-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7bea1-224">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="7bea1-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7bea1-225">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="7bea1-225">Test single sign-on</span></span>

<span data-ttu-id="7bea1-226">在本節中，您會使用存取面板來測試您的 Azure AD 單一登入設定。</span><span class="sxs-lookup"><span data-stu-id="7bea1-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7bea1-227">當您在存取面板中按一下 Envoy 圖示時，應該會自動登入 Envoy 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7bea1-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="7bea1-228">如需「存取面板」的詳細資訊，請參閱[存取面板簡介](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="7bea1-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7bea1-229">其他資源</span><span class="sxs-lookup"><span data-stu-id="7bea1-229">Additional resources</span></span>

* [<span data-ttu-id="7bea1-230">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="7bea1-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7bea1-231">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="7bea1-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

