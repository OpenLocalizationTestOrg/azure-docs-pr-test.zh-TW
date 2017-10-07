---
title: "教學課程：Azure Active Directory 與 SAP HANA 雲端平台整合 | Microsoft Docs"
description: "了解如何與 Azure Active Directory tooenable toouse SAP HANA Cloud Platform 的單一登入、 自動化佈建，以及更多 ！"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="48cb4-103">教學課程：Azure Active Directory 與 SAP HANA 雲端平台整合</span><span class="sxs-lookup"><span data-stu-id="48cb4-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="48cb4-104">本教學課程的 hello 目標是 Azure 與 SAP HANA Cloud Platform tooshow hello 整合。</span><span class="sxs-lookup"><span data-stu-id="48cb4-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="48cb4-105">本教學課程中所述的 hello 案例假設您已擁有 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="48cb4-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="48cb4-106">有效的 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="48cb4-106">A valid Azure subscription</span></span>
* <span data-ttu-id="48cb4-107">SAP HANA 雲端平台帳戶</span><span class="sxs-lookup"><span data-stu-id="48cb4-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="48cb4-108">完成本教學課程之後, hello 您已指派的 tooSAP HANA 雲端平台將會無法 toosingle 登入使用 hello hello 應用程式的 Azure AD 使用者[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="48cb4-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="48cb4-109">您需要 toodeploy 自己的應用程式，或訂閱 tooan 應用程式帳戶 tootest 單一登入您 SAP HANA 雲端平台上。</span><span class="sxs-lookup"><span data-stu-id="48cb4-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="48cb4-110">在此教學課程中，應用程式被部署在 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="48cb4-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="48cb4-111">本教學課程所述的 hello 案例包含下列建置組塊的 hello:</span><span class="sxs-lookup"><span data-stu-id="48cb4-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="48cb4-112">啟用 SAP HANA Cloud Platform 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="48cb4-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="48cb4-113">設定單一登入 (SSO)</span><span class="sxs-lookup"><span data-stu-id="48cb4-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="48cb4-114">指派角色 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="48cb4-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="48cb4-115">指派使用者</span><span class="sxs-lookup"><span data-stu-id="48cb4-115">Assigning users</span></span>

<span data-ttu-id="48cb4-116">![案例](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "案例")</span><span class="sxs-lookup"><span data-stu-id="48cb4-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="48cb4-117">啟用 SAP HANA Cloud Platform 的 hello 應用程式整合</span><span class="sxs-lookup"><span data-stu-id="48cb4-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="48cb4-118">本節 hello 目標是 toooutline 如何 SAP HANA Cloud Platform tooenable hello 應用程式整合。</span><span class="sxs-lookup"><span data-stu-id="48cb4-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="48cb4-119">**tooenable hello 應用程式整合，SAP HANA Cloud platform，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="48cb4-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="48cb4-120">在 hello Azure 管理入口網站中，在 hello 左側瀏覽窗格中，按一下  **Active Directory**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="48cb4-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="48cb4-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="48cb4-122">從 hello**目錄**清單中，選取 hello 想 tooenable 目錄整合的目錄。</span><span class="sxs-lookup"><span data-stu-id="48cb4-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="48cb4-123">tooopen hello 應用程式檢視在 hello 目錄檢視中，按一下**應用程式**hello 上方功能表中。</span><span class="sxs-lookup"><span data-stu-id="48cb4-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="48cb4-124">![應用程式](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "應用程式")</span><span class="sxs-lookup"><span data-stu-id="48cb4-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="48cb4-125">按一下**新增**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="48cb4-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="48cb4-126">![新增應用程式](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="48cb4-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="48cb4-127">在 [hello**怎麼辦想 toodo** ] 對話方塊中，按一下**從 hello 組件庫新增應用程式**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="48cb4-128">![從資源庫新增應用程式](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "從資源庫新增應用程式")</span><span class="sxs-lookup"><span data-stu-id="48cb4-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="48cb4-129">在 hello**搜尋方塊**，型別**SAP HANA Cloud Platform**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="48cb4-130">![應用程式資源庫](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "應用程式資源庫")</span><span class="sxs-lookup"><span data-stu-id="48cb4-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="48cb4-131">在 hello 結果窗格中，選取  **SAP HANA Cloud Platform**，然後按一下**完成**tooadd hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="48cb4-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="48cb4-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="48cb4-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="48cb4-133">設定單一登入</span><span class="sxs-lookup"><span data-stu-id="48cb4-133">Configure single sign-on</span></span>

<span data-ttu-id="48cb4-134">hello 本節目標在於的 toooutline tooenable 使用者 tooauthenticate tooSAP HANA 雲端平台與 Azure AD 的同盟，使用的帳戶如何 hello SAML 通訊協定為基礎。</span><span class="sxs-lookup"><span data-stu-id="48cb4-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="48cb4-135">此程序的一部分，您就需要的 tooupload base 64 編碼的憑證 tooyour SAP HANA Cloud Platform 租用戶。</span><span class="sxs-lookup"><span data-stu-id="48cb4-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="48cb4-136">如果您不熟悉這個程序，請參閱[如何 tooconvert 二進位憑證到文字檔案](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="48cb4-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="48cb4-137">**tooconfigure 單一登入，請執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="48cb4-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="48cb4-138">在 Azure 傳統入口網站，在 hello hello **SAP HANA Cloud Platform**應用程式整合頁面上，按一下 **設定單一登入**tooopen hello**設定單一登入**對話方塊。</span><span class="sxs-lookup"><span data-stu-id="48cb4-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="48cb4-139">![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="48cb4-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="48cb4-140">Hello 上**如何想您 tooSAP HANA 雲端平台上的使用者 toosign**頁面上，選取**Microsoft Azure AD 單一登入**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="48cb4-141">![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="48cb4-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="48cb4-142">在不同的網頁瀏覽器視窗中，登入在 https://account toohello SAP HANA Cloud Platform Cockpit。\<橫向主機\>.ondemand.com/cockpit (例如： *https://account.hanatrial.ondemand.com/cockpit*)。</span><span class="sxs-lookup"><span data-stu-id="48cb4-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="48cb4-143">按一下 hello**信任** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48cb4-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="48cb4-144">![信任](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "信任")</span><span class="sxs-lookup"><span data-stu-id="48cb4-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="48cb4-145">在信任管理區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="48cb4-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="48cb4-146">![取得中繼資料](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "取得中繼資料")</span><span class="sxs-lookup"><span data-stu-id="48cb4-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="48cb4-147">按一下 hello**本機服務提供者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48cb4-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="48cb4-148">toodownload hello SAP HANA Cloud Platform 中繼資料檔案中，按一下**取得中繼資料**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="48cb4-149">Hello 作用中的 Azure 傳統入口網站中，在 hello**設定應用程式 URL**頁面上，執行下列步驟，hello，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="48cb4-150">![設定應用程式 URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "設定應用程式 URL")</span><span class="sxs-lookup"><span data-stu-id="48cb4-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="48cb4-151">在 hello**登入 URL**文字方塊中，為您的使用者 toosign 所使用的型別 hello URL 您**SAP HANA Cloud Platform**應用程式。</span><span class="sxs-lookup"><span data-stu-id="48cb4-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="48cb4-152">這是 SAP HANA Cloud Platform 應用程式中某個受保護資源的 hello 帳戶特有 URL。</span><span class="sxs-lookup"><span data-stu-id="48cb4-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="48cb4-153">hello URL 根據下列模式的 hello: *https://\<applicationName\>\<accountName\>。\<橫向主機\>.ondemand.com/\<路徑\_至\_保護\_資源\>* (例如： *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="48cb4-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="48cb4-154">這是您需要 hello 使用者 tooauthenticate 的 SAP HANA Cloud Platform 應用程式中的 hello URL。</span><span class="sxs-lookup"><span data-stu-id="48cb4-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="48cb4-155">開啟 hello 下載 SAP HANA Cloud Platform 中繼資料檔案，然後再找出 hello **ns3: assertionconsumerservice**標記。</span><span class="sxs-lookup"><span data-stu-id="48cb4-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="48cb4-156">複製 hello hello 值**位置**屬性，然後再將它貼到 hello **SAP HANA Cloud Platform 回覆 URL**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="48cb4-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="48cb4-157">在 hello**於 SAP HANA Cloud Platform 設定單一登入**頁面、 toodownload 中繼資料，按一下**下載中繼資料**，然後儲存您的電腦上的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="48cb4-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="48cb4-158">![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="48cb4-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="48cb4-159">在 hello hello SAP HANA Cloud Platform Cockpit 上**本機服務提供者**區段中，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="48cb4-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="48cb4-160">![信任管理](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "信任管理")</span><span class="sxs-lookup"><span data-stu-id="48cb4-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="48cb4-161">按一下 [ **編輯**]。</span><span class="sxs-lookup"><span data-stu-id="48cb4-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="48cb4-162">針對 [組態類型]，選取 [自訂]。</span><span class="sxs-lookup"><span data-stu-id="48cb4-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="48cb4-163">做為**本機提供者名稱**，保留 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="48cb4-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="48cb4-164">toogenerate**簽署金鑰**和**簽署憑證**金鑰組，請按一下**產生金鑰組**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="48cb4-165">針對 [主體傳播]，選取 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="48cb4-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="48cb4-166">針對 [強制驗證]，選取 [已停用]。</span><span class="sxs-lookup"><span data-stu-id="48cb4-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="48cb4-167">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="48cb4-167">Click **Save**.</span></span>

9. <span data-ttu-id="48cb4-168">按一下 hello**信任身分識別提供者**索引標籤，然後再按一下**新增信任身分識別提供者**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="48cb4-169">![信任管理](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "信任管理")</span><span class="sxs-lookup"><span data-stu-id="48cb4-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="48cb4-170">toomanage hello 清單中的受信任的身分識別提供者，您需要 toohave hello 本機服務提供者 區段中選擇 hello 自訂組態類型。</span><span class="sxs-lookup"><span data-stu-id="48cb4-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="48cb4-171">預設組態類型，您會有非可編輯與隱含信任 toohello SAP ID 服務。</span><span class="sxs-lookup"><span data-stu-id="48cb4-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="48cb4-172">針對 [無]，您不具任何信任設定。</span><span class="sxs-lookup"><span data-stu-id="48cb4-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="48cb4-173">按一下 hello**一般**索引標籤，然後再按一下**瀏覽**tooupload hello 下載中繼資料檔案。</span><span class="sxs-lookup"><span data-stu-id="48cb4-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="48cb4-174">![信任管理](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "信任管理")</span><span class="sxs-lookup"><span data-stu-id="48cb4-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="48cb4-175">上傳 hello 中繼資料檔案之後, hello 值**單一登入 URL**，**單一登出 URL**和**簽署憑證**會自動填入。</span><span class="sxs-lookup"><span data-stu-id="48cb4-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="48cb4-176">按一下 hello**屬性** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48cb4-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="48cb4-177">在 hello**屬性**索引標籤上，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="48cb4-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="48cb4-178">![屬性](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "屬性")</span><span class="sxs-lookup"><span data-stu-id="48cb4-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="48cb4-179">按一下**新增屬性**，然後加入下列判斷提示型屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="48cb4-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="48cb4-180">判斷提示屬性</span><span class="sxs-lookup"><span data-stu-id="48cb4-180">Assertion Attribute</span></span> | <span data-ttu-id="48cb4-181">主體屬性</span><span class="sxs-lookup"><span data-stu-id="48cb4-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="48cb4-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span><span class="sxs-lookup"><span data-stu-id="48cb4-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="48cb4-183">firstname</span><span class="sxs-lookup"><span data-stu-id="48cb4-183">firstname</span></span> |
    | <span data-ttu-id="48cb4-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span><span class="sxs-lookup"><span data-stu-id="48cb4-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="48cb4-185">lastname</span><span class="sxs-lookup"><span data-stu-id="48cb4-185">lastname</span></span> |
    | <span data-ttu-id="48cb4-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="48cb4-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="48cb4-187">電子郵件</span><span class="sxs-lookup"><span data-stu-id="48cb4-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="48cb4-188">hello 組態的 hello 屬性取決於如何在 HCP 上的 hello 應用程式開發，也就是預期在 SAML 回應 hello 和 （主體屬性） 的名稱下他們存取 hello 程式碼中的此屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="48cb4-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="48cb4-189">hello**預設屬性**在 hello 螢幕擷取畫面是只供說明之用。</span><span class="sxs-lookup"><span data-stu-id="48cb4-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="48cb4-190">它不需要 toomake hello 案例的工作。</span><span class="sxs-lookup"><span data-stu-id="48cb4-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="48cb4-191">hello 名稱和值**主體屬性**示 hello 螢幕擷取畫面，取決於 hello 應用程式的開發方式。</span><span class="sxs-lookup"><span data-stu-id="48cb4-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="48cb4-192">您的應用程式很可能需要不同的對應。</span><span class="sxs-lookup"><span data-stu-id="48cb4-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="48cb4-193">在 Azure 傳統入口網站，在 hello hello**於 SAP HANA Cloud Platform 設定單一登入**頁面，選取 hello 單一登入組態確認，然後按**完成**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="48cb4-194">![設定單一登入](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "設定單一登入")</span><span class="sxs-lookup"><span data-stu-id="48cb4-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="48cb4-195">以判斷提示為基礎的群組</span><span class="sxs-lookup"><span data-stu-id="48cb4-195">Assertion-based groups</span></span>
<span data-ttu-id="48cb4-196">在選擇性的步驟中，您可以為 Azure Active Directory 識別提供者設定以判斷提示為基礎的群組。</span><span class="sxs-lookup"><span data-stu-id="48cb4-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="48cb4-197">使用 SAP HANA 雲端平台上的群組可讓您 toodynamically 指派一個或多個使用者 tooone 或多個角色，在 SAP HANA Cloud Platform 的應用程式，取決於中 hello SAML 屬性的值 2.0 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="48cb4-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="48cb4-198">例如，如果 hello 判斷提示包含 hello 屬性 」*合約 = 暫存*"，您可能要讓所有受影響的使用者 toobe 加入的 toohello 群組"*暫存*"。</span><span class="sxs-lookup"><span data-stu-id="48cb4-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="48cb4-199">hello 群組 」*暫存*」 可能包含一或多個角色部署 SAP HANA Cloud Platform 帳戶中的一個或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="48cb4-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="48cb4-200">當您想 toosimultaneously 指派許多使用者 tooone 或多個角色的應用程式在 SAP HANA Cloud Platform 帳戶中，請使用判斷提示型群組。</span><span class="sxs-lookup"><span data-stu-id="48cb4-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="48cb4-201">如果您想 tooassign 只有少數使用者 toospecific 角色數目，我們建議您直接在 hello 分派給他們"**授權**"hello SAP HANA Cloud Platform cockpit 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48cb4-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="48cb4-202">指派給某個角色 tooa 使用者</span><span class="sxs-lookup"><span data-stu-id="48cb4-202">Assign a role tooa user</span></span>
<span data-ttu-id="48cb4-203">在訂單 tooenable Azure AD 使用者 toolog 入 SAP HANA Cloud Platform，您必須指派 hello SAP HANA Cloud Platform toothem 中的角色。</span><span class="sxs-lookup"><span data-stu-id="48cb4-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="48cb4-204">**tooassign 角色 tooa 使用者時，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="48cb4-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="48cb4-205">登入 tooyour **SAP HANA Cloud Platform** cockpit。</span><span class="sxs-lookup"><span data-stu-id="48cb4-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="48cb4-206">執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="48cb4-206">Perform hello following:</span></span>
   
   <span data-ttu-id="48cb4-207">![授權](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "授權")</span><span class="sxs-lookup"><span data-stu-id="48cb4-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="48cb4-208">按一下 [授權]。</span><span class="sxs-lookup"><span data-stu-id="48cb4-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="48cb4-209">按一下 hello**使用者** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="48cb4-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="48cb4-210">在 hello**使用者**文字方塊中，型別 hello 使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="48cb4-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="48cb4-211">按一下**指派**tooassign hello 使用者 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="48cb4-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="48cb4-212">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="48cb4-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="48cb4-213">指派使用者</span><span class="sxs-lookup"><span data-stu-id="48cb4-213">Assign users</span></span>
<span data-ttu-id="48cb4-214">tootest 您的設定，您需要您想要使用您的應用程式存取 tooit 由將其指派的 tooallow toogrant hello Azure AD 使用者。</span><span class="sxs-lookup"><span data-stu-id="48cb4-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="48cb4-215">**tooassign 使用者 tooSAP HANA Cloud Platform 中，執行下列步驟的 hello:**</span><span class="sxs-lookup"><span data-stu-id="48cb4-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="48cb4-216">在 hello Azure 傳統入口網站，建立測試帳戶。</span><span class="sxs-lookup"><span data-stu-id="48cb4-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="48cb4-217">在 hello **SAP HANA Cloud Platform**應用程式整合頁面上，按一下 **指派使用者**。</span><span class="sxs-lookup"><span data-stu-id="48cb4-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="48cb4-218">![指派使用者](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "指派使用者")</span><span class="sxs-lookup"><span data-stu-id="48cb4-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="48cb4-219">選取您的測試使用者，請按一下**指派**，然後按一下**是**tooconfirm 作業。</span><span class="sxs-lookup"><span data-stu-id="48cb4-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="48cb4-220">![是](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "是")</span><span class="sxs-lookup"><span data-stu-id="48cb4-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="48cb4-221">如果您想 tootest SSO 設定，請開啟 hello 存取面板。</span><span class="sxs-lookup"><span data-stu-id="48cb4-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="48cb4-222">如需 hello 存取面板的詳細資訊，請參閱[簡介 toohello 存取面板](active-directory-saas-access-panel-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="48cb4-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

