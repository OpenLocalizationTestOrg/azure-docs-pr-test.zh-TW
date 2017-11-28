---
title: "教學課程：Azure Active Directory 與 Symantec Web Security Service (WSS) 整合 | Microsoft Docs"
description: "了解如何設定 Azure Active Directory 與 Symantec Web Security Service (WSS) 之間的單一登入。"
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 61576d3a915d209e7355e04432e586dcf66e7c5a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a><span data-ttu-id="0e199-103">教學課程：Azure Active Directory 與 Symantec Web Security Service (WSS) 整合</span><span class="sxs-lookup"><span data-stu-id="0e199-103">Tutorial: Azure Active Directory integration with Symantec Web Security Service (WSS)</span></span>

<span data-ttu-id="0e199-104">在本教學課程中，您將學習如何整合 Symantec Web Security Service (WSS) 帳戶與 Azure Active Directory (Azure AD) 帳戶，讓 WSS 可使用 SAML 驗證來驗證 Azure AD 中所佈建的使用者，並強制執行使用者或群組層級的原則規則。</span><span class="sxs-lookup"><span data-stu-id="0e199-104">In this tutorial, you will learn how to integrate your Symantec Web Security Service (WSS) account with your Azure Active Directory (Azure AD) account so that WSS can authenticate an end user provisioned in the Azure AD using SAML authentication and enforce user or group level policy rules.</span></span>

<span data-ttu-id="0e199-105">Symantec Web Security Service (WSS) 與 Azure AD 整合提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="0e199-105">Integrating Symantec Web Security Service (WSS) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e199-106">從 Azure AD 入口網站管理您的 WSS 帳戶使用的所有使用者和群組。</span><span class="sxs-lookup"><span data-stu-id="0e199-106">Manage all of the end users and groups used by your WSS account from your Azure AD portal.</span></span> 

- <span data-ttu-id="0e199-107">讓使用者可以使用其 Azure AD 認證在 WSS 中驗證其自身。</span><span class="sxs-lookup"><span data-stu-id="0e199-107">Allow the end users to authenticate themselves in WSS using their Azure AD credentials.</span></span>

- <span data-ttu-id="0e199-108">強制執行 WSS 帳戶中所定義的使用者和群組層級原則規則。</span><span class="sxs-lookup"><span data-stu-id="0e199-108">Enable the enforcement of user and group level policy rules defined in your WSS account.</span></span>

<span data-ttu-id="0e199-109">如果您想要了解有關 SaaS 應用程式與 Azure AD 之整合的更多詳細資料，請參閱[什麼是搭配 Azure Active Directory 的應用程式存取和單一登入](active-directory-appssoaccess-whatis.md)。</span><span class="sxs-lookup"><span data-stu-id="0e199-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e199-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="0e199-110">Prerequisites</span></span>

<span data-ttu-id="0e199-111">若要設定 Azure AD 與 Symantec Web Security Service (WSS) 整合，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="0e199-111">To configure Azure AD integration with Symantec Web Security Service (WSS), you need the following items:</span></span>

- <span data-ttu-id="0e199-112">Azure AD 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="0e199-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e199-113">Symantec Web Security Service (WSS) 帳戶</span><span class="sxs-lookup"><span data-stu-id="0e199-113">A Symantec Web Security Service (WSS) account</span></span>

> [!NOTE]
> <span data-ttu-id="0e199-114">若要測試本教學課程中的步驟，我們不建議使用目前正用於生產用途的 WSS 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0e199-114">To test the steps in this tutorial, we do not recommend using a WSS account that is currently being used for production purpose.</span></span>

<span data-ttu-id="0e199-115">若要測試本教學課程中的步驟，您應該遵循這些建議：</span><span class="sxs-lookup"><span data-stu-id="0e199-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e199-116">除非必要，否則請勿使用目前正用於生產用途的 WSS 帳戶來進行這項測試。</span><span class="sxs-lookup"><span data-stu-id="0e199-116">Do not use your WSS account that is currently being used for production purpose for this test unless it is necessary.</span></span>
- <span data-ttu-id="0e199-117">如果您沒有 Azure AD 試用環境，您可以[取得一個月試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="0e199-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e199-118">案例描述</span><span class="sxs-lookup"><span data-stu-id="0e199-118">Scenario description</span></span>
<span data-ttu-id="0e199-119">在本教學課程中，您會將 Azure AD 設定為能夠使用 Azure AD 帳戶中所定義的使用者認證來對 WSS 進行單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-119">In this tutorial, you will configure your Azure AD to enable single sign-on to WSS using the end user credentials defined in your Azure AD account.</span></span>
<span data-ttu-id="0e199-120">本教學課程中說明的案例由二個主要建置組塊組成：</span><span class="sxs-lookup"><span data-stu-id="0e199-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e199-121">從資源庫新增 Symantec Web Security Service (WSS) 應用程式</span><span class="sxs-lookup"><span data-stu-id="0e199-121">Adding the Symantec Web Security Service (WSS) app from the gallery</span></span>
2. <span data-ttu-id="0e199-122">設定並測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0e199-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-symantec-web-security-service-wss-from-the-gallery"></a><span data-ttu-id="0e199-123">從資源庫新增 Symantec Web Security Service (WSS)</span><span class="sxs-lookup"><span data-stu-id="0e199-123">Adding Symantec Web Security Service (WSS) from the gallery</span></span>
<span data-ttu-id="0e199-124">若要設定 Symantec Web Security Service (WSS) 與 Azure AD 整合，您需要從資源庫將 Symantec Web Security Service (WSS) 新增到受管理的 SaaS App 清單。</span><span class="sxs-lookup"><span data-stu-id="0e199-124">To configure the integration of Symantec Web Security Service (WSS) into Azure AD, you need to add Symantec Web Security Service (WSS) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e199-125">**若要從資源庫新增 Symantec Web Security Service (WSS)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e199-125">**To add Symantec Web Security Service (WSS) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e199-126">在 **[Azure 入口網站](https://portal.azure.com)**的左方瀏覽窗格中，按一下 [Azure Active Directory] 圖示。</span><span class="sxs-lookup"><span data-stu-id="0e199-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Azure Active Directory 按鈕][1]

2. <span data-ttu-id="0e199-128">瀏覽至 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0e199-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e199-129">然後移至 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0e199-129">Then go to **All applications**.</span></span>

    ![企業應用程式刀鋒視窗][2]
    
3. <span data-ttu-id="0e199-131">若要新增新的應用程式，請按一下對話方塊頂端的 [新增應用程式] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e199-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![新增應用程式按鈕][3]

4. <span data-ttu-id="0e199-133">在搜尋方塊中，輸入 **Symantec Web Security Service (WSS)**，從結果面板選取 [Symantec Web Security Service (WSS)]，然後按一下 [新增] 按鈕以新增應用程式。</span><span class="sxs-lookup"><span data-stu-id="0e199-133">In the search box, type **Symantec Web Security Service (WSS)**, select **Symantec Web Security Service (WSS)** from result panel then click **Add** button to add the application.</span></span>

    ![結果清單中的 Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0e199-135">設定和測試 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0e199-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0e199-136">在本節中，您會以名為 "Britta Simon" 的測試使用者為基礎，設定及測試與 Symantec Web Security Service (WSS) 搭配運作的 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-136">In this section, you configure and test Azure AD single sign-on with Symantec Web Security Service (WSS) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e199-137">若要讓單一登入運作，Azure AD 必須知道 Symantec Web Security Service (WSS) 與 Azure AD 中互相對應的使用者。</span><span class="sxs-lookup"><span data-stu-id="0e199-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Symantec Web Security Service (WSS) is to a user in Azure AD.</span></span> <span data-ttu-id="0e199-138">換句話說，必須在 Azure AD 使用者和 Symantec Web Security Service (WSS) 中的相關使用者之間建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0e199-138">In other words, a link relationship between an Azure AD user and the related user in Symantec Web Security Service (WSS) needs to be established.</span></span>

<span data-ttu-id="0e199-139">在 Symantec Web Security Service (WSS) 中，將**使用者名稱**的值指派為 Azure AD 中**使用者名稱**的值，以建立連結關聯性。</span><span class="sxs-lookup"><span data-stu-id="0e199-139">In Symantec Web Security Service (WSS), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0e199-140">若要使用 Symantec Web Security Service (WSS) 來設定並測試 Azure AD 單一登入，您需要完成下列建置組塊：</span><span class="sxs-lookup"><span data-stu-id="0e199-140">To configure and test Azure AD single sign-on with Symantec Web Security Service (WSS), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e199-141">**[設定 Azure AD 單一登入](#configure-azure-ad-single-sign-on)** - 讓您的使用者能夠使用此功能。</span><span class="sxs-lookup"><span data-stu-id="0e199-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0e199-142">**[建立 Azure AD 測試使用者](#create-an-azure-ad-test-user)** - 使用 Britta Simon 測試 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0e199-143">**[建立 Symantec Web Security Service (WSS) 測試使用者](#create-a-symantec-web-security-service-wss-test-user)** - 使 Symantec Web Security Service (WSS) 中對應的 Britta Simon 連結到該使用者在 Azure AD 中的代表項目。</span><span class="sxs-lookup"><span data-stu-id="0e199-143">**[Create a Symantec Web Security Service (WSS) test user](#create-a-symantec-web-security-service-wss-test-user)** - to have a counterpart of Britta Simon in Symantec Web Security Service (WSS) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0e199-144">**[指派 Azure AD 測試使用者](#assign-the-azure-ad-test-user)** - 讓 Britta Simon 能夠使用 Azure AD 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0e199-145">**[測試單一登入](#test-single-sign-on)**，驗證組態是否能運作。</span><span class="sxs-lookup"><span data-stu-id="0e199-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0e199-146">設定 Azure AD 單一登入</span><span class="sxs-lookup"><span data-stu-id="0e199-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0e199-147">在本節中，您會在 Azure 入口網站中啟用 Azure AD 單一登入，然後在您的 Symantec Web Security Service (WSS) 應用程式中設定單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Symantec Web Security Service (WSS) application.</span></span>

<span data-ttu-id="0e199-148">**若要使用 Symantec Web Security Service (WSS) 設定 Azure AD 單一登入，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e199-148">**To configure Azure AD single sign-on with Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="0e199-149">在 Azure 入口網站的 [Symantec Web Security Service]\(WSS\) 應用程式整合頁面上，按一下 [單一登入]。</span><span class="sxs-lookup"><span data-stu-id="0e199-149">In the Azure portal, on the **Symantec Web Security Service (WSS)** application integration page, click **Single sign-on**.</span></span>

    ![設定單一登入連結][4]

2. <span data-ttu-id="0e199-151">在 [單一登入] 對話方塊上，於 [模式] 選取 [SAML 登入]，以啟用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![單一登入對話方塊](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. <span data-ttu-id="0e199-153">在 [Symantec Web Security Service (WSS) 網域與 URL] 區段上，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0e199-153">On the **Symantec Web Security Service (WSS) Domain and URLs** section, perform the following steps:</span></span>

    ![Symantec Web Security Service (WSS) 的網域和 URL 單一登入資訊](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    <span data-ttu-id="0e199-155">a.</span><span class="sxs-lookup"><span data-stu-id="0e199-155">a.</span></span> <span data-ttu-id="0e199-156">在 [識別碼] 文字方塊中，輸入 URL：`https://saml.threatpulse.net:8443/saml/saml_realm`</span><span class="sxs-lookup"><span data-stu-id="0e199-156">In the **Identifier** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm`</span></span>

    <span data-ttu-id="0e199-157">b.</span><span class="sxs-lookup"><span data-stu-id="0e199-157">b.</span></span> <span data-ttu-id="0e199-158">在 [回覆 URL] 文字方塊中，輸入 URL：`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span><span class="sxs-lookup"><span data-stu-id="0e199-158">In the **Reply URL** textbox, type the URL: `https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`</span></span>

    > [!NOTE]
    > <span data-ttu-id="0e199-159">如果 [識別碼] 和 [回覆 URL] 的值因為某些原因而沒有作用，請連絡 [Symantec Web Security Service (WSS) 客戶支援小組](https://www.symantec.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="0e199-159">Please contact the [Symantec Web Security Service (WSS) Client support team](https://www.symantec.com/contact-us) if the values for the **Identifier** and **Reply URL** are not working for some reason.</span></span>

4. <span data-ttu-id="0e199-160">在 [SAML 簽署憑證] 區段上，按一下 [中繼資料 XML]，然後將中繼資料檔案儲存在您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="0e199-160">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![憑證下載連結](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. <span data-ttu-id="0e199-162">按一下 [儲存]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e199-162">Click **Save** button.</span></span>

    ![設定單一登入儲存按鈕](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="0e199-164">若要在 Symantec Web Security Service (WSS) 端設定單一登入，請參閱 WSS 線上文件。</span><span class="sxs-lookup"><span data-stu-id="0e199-164">To configure single sign-on on the Symantec Web Security Service (WSS) side, refer to the WSS online documentation.</span></span> <span data-ttu-id="0e199-165">所下載的**中繼資料 XML** 檔案必須匯入到 WSS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0e199-165">The downloaded **Metadata XML** file will need to be imported into the WSS portal.</span></span> <span data-ttu-id="0e199-166">如果您需要協助進行 WSS 入口網站設定，請連絡 [Symantec Web Security Service (WSS) 支援小組](https://www.symantec.com/contact-us)。</span><span class="sxs-lookup"><span data-stu-id="0e199-166">Contact the [Symantec Web Security Service (WSS) support team](https://www.symantec.com/contact-us) if you need assistance with the configuration on the WSS portal.</span></span>

> [!TIP]
> <span data-ttu-id="0e199-167">現在，當您設定此應用程式時，在 [Azure 入口網站](https://portal.azure.com)內即可閱讀這些指示的簡要版本！</span><span class="sxs-lookup"><span data-stu-id="0e199-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0e199-168">從 [Active Directory] > [企業應用程式] 區段新增此應用程式之後，只要按一下 [單一登入] 索引標籤，即可透過底部的 [組態] 區段存取內嵌的文件。</span><span class="sxs-lookup"><span data-stu-id="0e199-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0e199-169">您可以從以下連結閱讀更多有關內嵌文件功能的資訊：[Azure AD 內嵌文件]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e199-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0e199-170">建立 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0e199-170">Create an Azure AD test user</span></span>

<span data-ttu-id="0e199-171">本節的目標是要在 Azure 入口網站中建立一個名為 Britta Simon 的測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0e199-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![建立 Azure AD 測試使用者][100]

<span data-ttu-id="0e199-173">**若要在 Azure AD 中建立測試使用者，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e199-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e199-174">在 Azure 入口網站的左窗格中，按一下 [Azure Active Directory] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e199-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Azure Active Directory 按鈕](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="0e199-176">若要顯示使用者清單，請移至 [使用者和群組]，然後按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="0e199-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![[使用者和群組] 與 [所有使用者] 連結](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="0e199-178">若要開啟 [使用者] 對話方塊，按一下 [所有使用者] 對話方塊頂端的 [新增]。</span><span class="sxs-lookup"><span data-stu-id="0e199-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![[新增] 按鈕](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="0e199-180">在 [使用者] 對話方塊中，執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0e199-180">In the **User** dialog box, perform the following steps:</span></span>

    ![[使用者] 對話方塊](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    <span data-ttu-id="0e199-182">a.</span><span class="sxs-lookup"><span data-stu-id="0e199-182">a.</span></span> <span data-ttu-id="0e199-183">在 [名稱] 方塊中，輸入 **BrittaSimon**。</span><span class="sxs-lookup"><span data-stu-id="0e199-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e199-184">b.</span><span class="sxs-lookup"><span data-stu-id="0e199-184">b.</span></span> <span data-ttu-id="0e199-185">在 [使用者名稱] 方塊中，輸入使用者 Britta Simon 的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="0e199-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="0e199-186">c.</span><span class="sxs-lookup"><span data-stu-id="0e199-186">c.</span></span> <span data-ttu-id="0e199-187">選取 [顯示密碼] 核取方塊，然後記下 [密碼] 方塊中顯示的值。</span><span class="sxs-lookup"><span data-stu-id="0e199-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="0e199-188">d.</span><span class="sxs-lookup"><span data-stu-id="0e199-188">d.</span></span> <span data-ttu-id="0e199-189">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="0e199-189">Click **Create**.</span></span>
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a><span data-ttu-id="0e199-190">建立 Symantec Web Security Service (WSS) 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0e199-190">Create a Symantec Web Security Service (WSS) test user</span></span>

<span data-ttu-id="0e199-191">在本節中，您要在 Symantec Web Security Service (WSS) 中建立名為 Britta Simon 的使用者。</span><span class="sxs-lookup"><span data-stu-id="0e199-191">In this section, you create a user called Britta Simon in Symantec Web Security Service (WSS).</span></span> <span data-ttu-id="0e199-192">您可以在 WSS 入口網站中手動建立對應的使用者名稱，您也可以等候幾分鐘 (~ 15 分鐘)，讓 Azure AD 中佈建的使用者/群組同步處理至 WSS 入口網站。</span><span class="sxs-lookup"><span data-stu-id="0e199-192">The corresponding end username can be manually created in the WSS portal or you can wait for the users/groups provisioned in the Azure AD to be synchronized to the WSS portal after a few minutes (~15 minutes).</span></span> <span data-ttu-id="0e199-193">您必須先建立和啟動使用者，然後才能使用單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-193">Users must be created and activated before you use single sign-on.</span></span> <span data-ttu-id="0e199-194">將用來瀏覽網站的使用者電腦公用 IP 位址也必須佈建到 Symantec Web Security Service (WSS) 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0e199-194">The public IP address of the end user machine, which will be used to browse websites also need to be provisioned in the Symantec Web Security Service (WSS) portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0e199-195">請[按一下這裡](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1)以取得您機器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0e199-195">Please [click here](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) to get your machine's public IPaddress.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0e199-196">指派 Azure AD 測試使用者</span><span class="sxs-lookup"><span data-stu-id="0e199-196">Assign the Azure AD test user</span></span>

<span data-ttu-id="0e199-197">在本節中，您會將 Symantec Web Security Service (WSS) 的存取權授與 Britta Simon，讓她能夠使用 Azure 單一登入。</span><span class="sxs-lookup"><span data-stu-id="0e199-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Symantec Web Security Service (WSS).</span></span>

![指派使用者角色][200] 

<span data-ttu-id="0e199-199">**若要將 Britta Simon 指派給 Symantec Web Security Service (WSS)，請執行下列步驟：**</span><span class="sxs-lookup"><span data-stu-id="0e199-199">**To assign Britta Simon to Symantec Web Security Service (WSS), perform the following steps:**</span></span>

1. <span data-ttu-id="0e199-200">在 Azure 入口網站中，開啟應用程式檢視，接著瀏覽至目錄檢視並移至 [企業應用程式]，然後按一下 [所有應用程式]。</span><span class="sxs-lookup"><span data-stu-id="0e199-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![指派使用者][201] 

2. <span data-ttu-id="0e199-202">在應用程式清單中，選取 [Symantec Web Security Service (WSS)]。</span><span class="sxs-lookup"><span data-stu-id="0e199-202">In the applications list, select **Symantec Web Security Service (WSS)**.</span></span>

    ![應用程式清單中的 [Symantec Web Security Service (WSS)] 連結](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. <span data-ttu-id="0e199-204">在左側功能表中，按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0e199-204">In the menu on the left, click **Users and groups**.</span></span>

    ![[使用者和群組] 連結][202]

4. <span data-ttu-id="0e199-206">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e199-206">Click **Add** button.</span></span> <span data-ttu-id="0e199-207">然後選取 [新增指派] 對話方塊上的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="0e199-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![[新增指派] 窗格][203]

5. <span data-ttu-id="0e199-209">在 [使用者和群組] 對話方塊上，選取 [使用者] 清單中的 [Britta Simon]。</span><span class="sxs-lookup"><span data-stu-id="0e199-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0e199-210">按一下 [使用者和群組] 對話方塊上的 [選取] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e199-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0e199-211">按一下 [新增指派] 對話方塊上的 [指派] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0e199-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0e199-212">測試單一登入</span><span class="sxs-lookup"><span data-stu-id="0e199-212">Test single sign-on</span></span>

<span data-ttu-id="0e199-213">在本節中，因為您已將 WSS 帳戶設定為要使用 Azure AD 來進行 SAML 驗證，您將會測試單一登入功能。</span><span class="sxs-lookup"><span data-stu-id="0e199-213">In this section, you'll test the single sign-on functionality now that you've configured your WSS account to use your Azure AD for SAML authentication.</span></span>

<span data-ttu-id="0e199-214">在將網頁瀏覽器設定為將流量 Proxy 處理至 WSS 後，如果您開啟網頁瀏覽器並嘗試瀏覽至網站，則系統會將您重新導向至 Azure 的登入頁面。</span><span class="sxs-lookup"><span data-stu-id="0e199-214">After you have configured your web browser to proxy traffic to WSS, when you open your web browser and try to browse to a site then you'll be redirected to the Azure sign-on page.</span></span> <span data-ttu-id="0e199-215">請輸入已佈建到 Azure AD 之測試使用者 (也就是 BrittaSimon) 的認證以及相關聯的密碼。</span><span class="sxs-lookup"><span data-stu-id="0e199-215">Enter the credentials of the test end user that has been provisioned in the Azure AD (that is, BrittaSimon) and associated password.</span></span> <span data-ttu-id="0e199-216">通過驗證之後，您就可以瀏覽至您選擇的網站。</span><span class="sxs-lookup"><span data-stu-id="0e199-216">Once authenticated, you'll be able to browse to the website that you chose.</span></span> <span data-ttu-id="0e199-217">如果您在 WSS 端建立原則規則以阻止 BrittaSimon 瀏覽至特定網站，則當您嘗試以 BrittaSimon 這位使用者的身分瀏覽至該網站時，您應該會看見 WSS 封鎖頁面。</span><span class="sxs-lookup"><span data-stu-id="0e199-217">Should you create a policy rule on the WSS side to block BrittaSimon from browsing to a particular site then you should see the WSS block page when you attempt to browse to that site as user BrittaSimon.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e199-218">其他資源</span><span class="sxs-lookup"><span data-stu-id="0e199-218">Additional resources</span></span>

* [<span data-ttu-id="0e199-219">如何與 Azure Active Directory 整合 SaaS 應用程式的教學課程清單</span><span class="sxs-lookup"><span data-stu-id="0e199-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0e199-220">什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？</span><span class="sxs-lookup"><span data-stu-id="0e199-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

