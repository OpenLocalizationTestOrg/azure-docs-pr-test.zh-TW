---
title: "設定具名的驗證認證 | Microsoft Docs"
description: "了解如何提供 Visual Studio 可用來向 Azure 驗證要求的認證，以便將應用程式從 Visual Studio 發佈至 Azure，或用來監視現有的雲端服務。 "
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
ms.openlocfilehash: c486676a70e195ec85ad40540ea4b7caaa86bc48
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="setting-up-named-authentication-credentials"></a><span data-ttu-id="c064c-103">設定具名的驗證認證</span><span class="sxs-lookup"><span data-stu-id="c064c-103">Setting Up Named Authentication Credentials</span></span>
<span data-ttu-id="c064c-104">若要將應用程式從 Visual Studio 發佈至 Azure，或若要監視現有的雲端服務，您必須提供 Visual Studio 可用來向 Azure 驗證要求的認證。</span><span class="sxs-lookup"><span data-stu-id="c064c-104">To publish an application to Azure from Visual Studio or to monitor an existing cloud service, you must provide credentials that Visual Studio can use to authenticate requests to Azure.</span></span> <span data-ttu-id="c064c-105">您可以從 Visual Studio 中的幾個位置登入並提供這些認證。</span><span class="sxs-lookup"><span data-stu-id="c064c-105">There are several places in Visual Studio where you can sign in to provide these credentials.</span></span> <span data-ttu-id="c064c-106">例如，從 [伺服器總管] 中，您可以開啟 [Azure] 節點的捷徑功能表，並選擇 [連線至 Microsoft Azure 訂用帳戶...]。登入時，您可以在 Visual Studio 中取得與 Azure 帳戶相關聯的訂用帳戶資訊，而且接下來您無需執行任何動作。</span><span class="sxs-lookup"><span data-stu-id="c064c-106">For example, from the Server Explorer, you can open the shortcut menu for the **Azure** node and choose **Connect to Microsoft Azure Subscription...**. When you sign in, the subscription information associated with your Azure account is available in Visual Studio, and there is nothing more you have to do.</span></span>

<span data-ttu-id="c064c-107">Azure Tools 也支援像以前一樣使用訂用帳戶檔案 (.publishsettings 檔案) 提供認證。</span><span class="sxs-lookup"><span data-stu-id="c064c-107">Azure Tools also supports an older way of providing credentials, using the subscription file (.publishsettings file).</span></span> <span data-ttu-id="c064c-108">本主題將說明此方法，Azure SDK 2.2 中仍支援此方法。</span><span class="sxs-lookup"><span data-stu-id="c064c-108">This topic describes this method, which is still supported in Azure SDK 2.2.</span></span>

<span data-ttu-id="c064c-109">向 Azure 驗證需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="c064c-109">The following items are required for authentication to Azure:</span></span>

* <span data-ttu-id="c064c-110">訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="c064c-110">Your subscription ID</span></span>
* <span data-ttu-id="c064c-111">有效的 X.509 v3 憑證</span><span class="sxs-lookup"><span data-stu-id="c064c-111">A valid X.509 v3 certificate</span></span>

> [!NOTE]
> <span data-ttu-id="c064c-112">X.509 v3 憑證的金鑰長度必須至少為 2048 位元。</span><span class="sxs-lookup"><span data-stu-id="c064c-112">The length of the X.509 v3 certificate's key must be at least 2048 bits.</span></span> <span data-ttu-id="c064c-113">Azure 將會拒絕任何不符合此需求或無效的憑證。</span><span class="sxs-lookup"><span data-stu-id="c064c-113">Azure will reject any certificate that doesn’t meet this requirement or that isn’t valid.</span></span>
>
>

<span data-ttu-id="c064c-114">Visual Studio 會使用您的訂用帳戶識別碼連同憑證資料做為認證。</span><span class="sxs-lookup"><span data-stu-id="c064c-114">Visual Studio uses your subscription ID together with the certificate data as credentials.</span></span> <span data-ttu-id="c064c-115">包含憑證公開金鑰的訂用帳戶檔案 (.publishsettings 檔案) 會參考適當的認證。</span><span class="sxs-lookup"><span data-stu-id="c064c-115">The appropriate credentials are referenced in the subscription file (.publishsettings file), which contains a public key for the certificate.</span></span> <span data-ttu-id="c064c-116">訂用帳戶檔案可以包含多個訂用帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="c064c-116">The subscription file can contain credentials for more than one subscription.</span></span>

<span data-ttu-id="c064c-117">您可以在 [新增/編輯訂用帳戶]  對話方塊中編輯訂用帳戶資訊，本主題稍後會有說明。</span><span class="sxs-lookup"><span data-stu-id="c064c-117">You can edit the subscription information from the **New/Edit Subscription** dialog box, as explained later in this topic.</span></span>

<span data-ttu-id="c064c-118">如果您想要自行建立憑證，您可以參考[建立及上傳 Azure 的管理憑證](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx)中的指示，然後手動將憑證上傳至 [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="c064c-118">If you want to create a certificate yourself, you can refer to the instructions in [Create and Upload a Management Certificate for Azure](https://msdn.microsoft.com/library/windowsazure/gg551722.aspx) and then manually upload the certificate to the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>

> [!NOTE]
> <span data-ttu-id="c064c-119">Visual Studio 為管理雲端服務所需的這些認證，與針對 Azure 儲存體服務驗證要求所需的認證是不同的。</span><span class="sxs-lookup"><span data-stu-id="c064c-119">These credentials that Visual Studio requires to manage your cloud services aren’t the same credentials that are required to authenticate a request against the Azure storage services.</span></span>
>
>

## <a name="import-set-up-or-edit-authentication-credentials-in-visual-studio"></a><span data-ttu-id="c064c-120">在 Visual Studio 中設匯入、設定或編輯驗證認證</span><span class="sxs-lookup"><span data-stu-id="c064c-120">Import, set up, or edit authentication credentials in Visual Studio</span></span>
<span data-ttu-id="c064c-121">您可以在 [新增訂用帳戶] 對話方塊中匯入、設定或修改您的驗證認證，此對話方塊會在您執行下列動作時出現：</span><span class="sxs-lookup"><span data-stu-id="c064c-121">You can import, set up, or modify your authentication credentials in the **New Subscription** dialog box, which appears if you perform the following action:</span></span>

* <span data-ttu-id="c064c-122">在 [伺服器總管] 中，開啟 **Azure** 節點的捷徑功能表，選擇 [管理及篩選訂閱...]，再選擇 [憑證] 索引標籤，然後執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="c064c-122">In **Server Explorer**, open the shortcut menu for the **Azure** node, choose **Manage and Filter Subscriptions...**, choose the **Certificates** tab, and do one of the following:</span></span>

    * <span data-ttu-id="c064c-123">選擇 [匯入] 以開啟 [匯入 Microsoft Azure 訂用帳戶] 對話方塊，您可以為目前載入的訂用帳戶從中訂用帳戶檔案、瀏覽其下載位置，再匯入以用於驗證。</span><span class="sxs-lookup"><span data-stu-id="c064c-123">Choose **Import** to open the Import Microsoft Azure Subscriptions dialog where you can download the  subscriptions file for the currently loaded subscription, browse to its download location, and then import it for use in authentication.</span></span>
    * <span data-ttu-id="c064c-124">選擇 [新增] 以開啟 [新增訂用帳戶] 對話方塊，您可以從中設定新的訂用帳戶以用於驗證。</span><span class="sxs-lookup"><span data-stu-id="c064c-124">Choose **New** to open the New Subscription dialog where you can set up a new subscription for use in authentication.</span></span>
    * <span data-ttu-id="c064c-125">選擇 [編輯] (選擇作用中的訂用帳戶之後) 以開啟 [編輯訂用帳戶] 對話方塊，您可以從中編輯現有的訂用帳戶以用於驗證。</span><span class="sxs-lookup"><span data-stu-id="c064c-125">Choose **Edit** (after choosing your active subscription) to open the Edit Subscription dialog where you can edit an existing subscription for use in authentication.</span></span> 

<span data-ttu-id="c064c-126">下列程序假設 [新增訂用帳戶]  對話方塊已開啟。</span><span class="sxs-lookup"><span data-stu-id="c064c-126">The following procedure assumes that the **New Subscription** dialog box is open.</span></span>

### <a name="to-set-up-authentication-credentials-in-visual-studio"></a><span data-ttu-id="c064c-127">在 Visual Studio 中設定驗證認證</span><span class="sxs-lookup"><span data-stu-id="c064c-127">To set up authentication credentials in Visual Studio</span></span>
1. <span data-ttu-id="c064c-128">在驗證清單的 [選取現有憑證]  中選擇憑證。</span><span class="sxs-lookup"><span data-stu-id="c064c-128">In the **Select an existing certificate** for authentication list, choose a certificate.</span></span>
2. <span data-ttu-id="c064c-129">選擇 [複製完整路徑] 連結。</span><span class="sxs-lookup"><span data-stu-id="c064c-129">Choose the **Copy the full path** link.</span></span> <span data-ttu-id="c064c-130">憑證 (.cer 檔案) 的路徑便會複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="c064c-130">The path for the certificate (.cer file) is copied to the Clipboard.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c064c-131">若要從 Visual Studio 發佈 Azure 應用程式，您必須將此憑證上傳至 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="c064c-131">To publish your Azure application from Visual Studio, you must upload this certificate to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   >
   >
3. <span data-ttu-id="c064c-132">將憑證上傳到 Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="c064c-132">To upload the certificate to the Azure portal:</span></span>

   1. <span data-ttu-id="c064c-133">開啟 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)。</span><span class="sxs-lookup"><span data-stu-id="c064c-133">Open the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
   2. <span data-ttu-id="c064c-134">如果出現提示，請登入入口網站，然後瀏覽至 [設定]、[管理憑證]。</span><span class="sxs-lookup"><span data-stu-id="c064c-134">If prompted, sign in to the portal and then navigate to **Settings**, **Management Certificates**.</span></span>
   3. <span data-ttu-id="c064c-135">在 [管理憑證] 窗格中，選擇 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="c064c-135">In the Management certificates pane, choose **Upload**.</span></span>
   4. <span data-ttu-id="c064c-136">選取您的 Azure 訂用帳戶，貼上您剛剛建立之 .cer 檔案的完整路徑，並選擇 [上傳]。</span><span class="sxs-lookup"><span data-stu-id="c064c-136">Select your Azure subscription, paste the full path of the .cer file that you just created, and choose **Upload**.</span></span>
