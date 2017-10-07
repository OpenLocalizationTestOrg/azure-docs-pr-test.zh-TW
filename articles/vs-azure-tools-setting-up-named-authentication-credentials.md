---
title: "設定具名驗證認證 aaaSetting |Microsoft 文件"
description: "了解 Visual Studio 可以使用 tooauthenticate 要求 tooAzure toopublish 從 Visual Studio 或 toomonitor 的現有應用程式 tooAzure tootooprovide 認證如何雲端服務... "
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 61570907-42a1-40e8-bcd6-952b21a55786
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/22/2017
ms.author: kraigb
ms.openlocfilehash: 3cc147a2f7a3e766293ca282f56078cf24281346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="472df-103">設定具名的驗證認證</span><span class="sxs-lookup"><span data-stu-id="472df-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="472df-104">從 Visual Studio 或 toomonitor 現有的雲端服務應用程式 tooAzure toopublish 中，您必須提供認證，Visual Studio 可以使用 tooauthenticate 要求 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="472df-104">toopublish an application tooAzure from Visual Studio or toomonitor an existing cloud service, you must provide credentials that Visual Studio can use tooauthenticate requests tooAzure.</span></span> <span data-ttu-id="472df-105">有幾個位置，在 Visual Studio 中，您可以登入 tooprovide 中這些認證。</span><span class="sxs-lookup"><span data-stu-id="472df-105">There are several places in Visual Studio where you can sign in tooprovide these credentials.</span></span> <span data-ttu-id="472df-106">例如，hello 伺服器總管] 中，您可以從開啟 hello 的 hello 快顯功能表**Azure**節點，然後選擇 [**連接 tooMicrosoft Azure 訂用帳戶...**.當您登入時，hello 與您的 Azure 帳戶相關聯的訂用帳戶資訊使用在 Visual Studio 中，沒有任何多個具有 toodo。</span><span class="sxs-lookup"><span data-stu-id="472df-106">For example, from hello Server Explorer, you can open hello shortcut menu for hello **Azure** node and choose **Connect tooMicrosoft Azure Subscription...**. When you sign in, hello subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have toodo.</span></span>

<span data-ttu-id="472df-107">Azure Tools 還支援提供的認證，較舊的方式使用 hello 訂用帳戶檔案 （.publishsettings 檔案）。</span><span class="sxs-lookup"><span data-stu-id="472df-107">Azure Tools also supports an older way of providing credentials, using hello subscription file (.publishsettings file).</span></span> <span data-ttu-id="472df-108">本主題將說明此方法，Azure SDK 2.2 中仍支援此方法。</span><span class="sxs-lookup"><span data-stu-id="472df-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="472df-109">hello 下列項目所需的驗證 tooAzure:</span><span class="sxs-lookup"><span data-stu-id="472df-109">hello following items are required for authentication tooAzure:</span></span>

* <span data-ttu-id="472df-110">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="472df-110">Your subscription ID</span></span>
* <span data-ttu-id="472df-111">有效的 X.509 v3 憑證</span><span class="sxs-lookup"><span data-stu-id="472df-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="472df-112">hello hello X.509 v3 憑證的金鑰長度必須至少為 2048 個位元。</span><span class="sxs-lookup"><span data-stu-id="472df-112">hello length of hello X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="472df-113">Azure 將會拒絕任何不符合此需求或無效的憑證。</span><span class="sxs-lookup"><span data-stu-id="472df-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="472df-114">Visual Studio 會使用您的訂用帳戶 ID 與 hello 憑證資料一起做為認證。</span><span class="sxs-lookup"><span data-stu-id="472df-114">Visual Studio uses your subscription ID together with hello certificate data as credentials.</span></span> <span data-ttu-id="472df-115">hello 適當的認證會在 hello 訂用帳戶檔案 （.publishsettings 檔案），其中包含公開金鑰 hello 憑證參考。</span><span class="sxs-lookup"><span data-stu-id="472df-115">hello appropriate credentials are referenced in hello subscription file (.publishsettings file), which contains a public key for hello certificate.</span></span> <span data-ttu-id="472df-116">hello 訂閱檔案可以包含多個訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="472df-116">hello subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="472df-117">您可以編輯 hello 訂用帳戶資訊從 hello**新增/編輯訂用帳戶**對話方塊中，在本主題稍後所述。</span><span class="sxs-lookup"><span data-stu-id="472df-117">You can edit hello subscription information from hello **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="472df-118">如果您想 toocreate 憑證自己，您可以參考中的 toohello 指示[建立及上傳 Azure 的管理憑證](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx)然後再手動上傳 hello 憑證 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="472df-118">If you want toocreate a certificate yourself, you can refer toohello instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload hello certificate toohello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="472df-119">Visual Studio 需要您的雲端服務不是的 toomanage 這些認證 hello 必要的 tooauthenticate 的相同認證對 hello Azure 儲存體服務提出的要求。</span><span class="sxs-lookup"><span data-stu-id="472df-119">These credentials that Visual Studio requires toomanage your cloud services aren’t hello same credentials that are required tooauthenticate a request against hello Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="472df-120">在 Visual Studio 中設匯入、設定或編輯驗證認證</span><span class="sxs-lookup"><span data-stu-id="472df-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="472df-121">您可以匯入、 設定，或修改您的驗證認證，在 hello**新訂用帳戶**對話方塊中，會顯示您執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="472df-121">You can import, set up, or modify your authentication credentials in hello **New Subscription** dialog box, which appears if you perform hello following action:</span></span>

* <span data-ttu-id="472df-122">在**伺服器總管**，開啟 hello 的 hello 快顯功能表**Azure**  節點，選擇**管理和篩選訂閱...**，選擇 hello**憑證**索引標籤，然後執行 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="472df-122">In **Server Explorer**, open hello shortcut menu for hello **Azure** node, choose **Manage and Filter Subscriptions...**, choose hello **Certificates** tab, and do one of hello following:</span></span>

    * <span data-ttu-id="472df-123">選擇**匯入**tooopen hello 匯入的 Microsoft Azure 訂用帳戶 對話方塊，您可以下載 hello 的 hello 訂用帳戶檔案目前載入的訂用帳戶中，瀏覽 tooits 下載位置，並將它匯入，以用於驗證。</span><span class="sxs-lookup"><span data-stu-id="472df-123">Choose **Import** tooopen hello Import Microsoft Azure Subscriptions dialog where you can download hello  subscriptions file for hello currently loaded subscription, browse tooits download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="472df-124">選擇**新增**tooopen hello 新訂用帳戶 對話方塊，您可以設定用於驗證的新訂閱。</span><span class="sxs-lookup"><span data-stu-id="472df-124">Choose **New** tooopen hello New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="472df-125">選擇**編輯**（之後，選擇您的作用中訂用帳戶） tooopen hello 編輯訂用帳戶 對話方塊，您可以編輯用於驗證現有的訂閱。</span><span class="sxs-lookup"><span data-stu-id="472df-125">Choose **Edit** (after choosing your active subscription) tooopen hello Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="472df-126">hello 下列程序會假設該 hello**新訂用帳戶**對話方塊為開啟。</span><span class="sxs-lookup"><span data-stu-id="472df-126">hello following procedure assumes that hello **New Subscription** dialog box is open.</span></span>

### <a name="tooset-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="472df-127">在 Visual Studio 中的驗證認證 tooset</span><span class="sxs-lookup"><span data-stu-id="472df-127">tooset up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="472df-128">在 [hello**選取現有憑證**驗證] 清單中，選擇憑證。</span><span class="sxs-lookup"><span data-stu-id="472df-128">In hello **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="472df-129">選擇 hello**複製 hello 完整路徑**連結。</span><span class="sxs-lookup"><span data-stu-id="472df-129">Choose hello **Copy hello full path** link.</span></span> <span data-ttu-id="472df-130">hello 憑證 （.cer 檔案） 的 hello 路徑是複製的 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="472df-130">hello path for hello certificate (.cer file) is copied toohello Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="472df-131">toopublish Azure 應用程式從 Visual Studio 中，您必須上傳此憑證 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="472df-131">toopublish your Azure application from Visual Studio, you must upload this certificate toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="472df-132">tooupload hello 憑證 toohello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="472df-132">tooupload hello certificate toohello Azure portal:</span></span>

   1. <span data-ttu-id="472df-133">開啟 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="472df-133">Open hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="472df-134">如果出現提示，請登入 toohello 入口網站，然後瀏覽過**設定**，**管理憑證**。</span><span class="sxs-lookup"><span data-stu-id="472df-134">If prompted, sign in toohello portal and then navigate too**Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="472df-135">在 hello 管理憑證 窗格中，選擇 **上傳**。</span><span class="sxs-lookup"><span data-stu-id="472df-135">In hello Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="472df-136">選取您的 Azure 訂閱，貼上 hello 剛 hello.cer 檔案的完整路徑建立，並選擇**上傳**。</span><span class="sxs-lookup"><span data-stu-id="472df-136">Select your Azure subscription, paste hello full path of hello .cer file that you just created, and choose **Upload**.</span></span>
