---
title: "使用 aaaGet 資料 hello Azure AD 報告 API 使用的憑證 |Microsoft 文件"
description: "說明如何 toouse hello Azure AD 報告 API 的憑證認證 tooget 資料不需要使用者介入的目錄。"
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="2a87f-103">取得憑證搭配使用 hello Azure AD 報告 API 的資料</span><span class="sxs-lookup"><span data-stu-id="2a87f-103">Get data using hello Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="2a87f-104">本文將討論如何 toouse hello Azure AD 報告 API 的憑證認證 tooget 資料不需要使用者介入的目錄。</span><span class="sxs-lookup"><span data-stu-id="2a87f-104">This article discusses how toouse hello Azure AD Reporting API with certificate credentials tooget data from directories without user intervention.</span></span> 

## <a name="use-hello-azure-ad-reporting-api"></a><span data-ttu-id="2a87f-105">使用 hello Azure AD 報告 API</span><span class="sxs-lookup"><span data-stu-id="2a87f-105">Use hello Azure AD Reporting API</span></span> 
<span data-ttu-id="2a87f-106">Azure AD 報告 API 需要您先完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a87f-106">Azure AD Reporting API requires that you complete hello following steps:</span></span>
 *  <span data-ttu-id="2a87f-107">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="2a87f-107">Install prerequisites</span></span>
 *  <span data-ttu-id="2a87f-108">設定應用程式中的 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="2a87f-108">Set hello certificate in your app</span></span>
 *  <span data-ttu-id="2a87f-109">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="2a87f-109">Get an access token</span></span>
 *  <span data-ttu-id="2a87f-110">使用 hello 存取語彙基元 toocall hello Graph API</span><span class="sxs-lookup"><span data-stu-id="2a87f-110">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="2a87f-111">如需原始程式碼的相關資訊，請參閱[運用報告 API 模組](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils)。</span><span class="sxs-lookup"><span data-stu-id="2a87f-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="2a87f-112">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="2a87f-112">Install prerequisites</span></span>
<span data-ttu-id="2a87f-113">您將需要 Azure AD PowerShell V2 toohave 和 AzureADUtils 模組安裝。</span><span class="sxs-lookup"><span data-stu-id="2a87f-113">You will need toohave Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="2a87f-114">下載並安裝 Azure AD Powershell V2、 在 hello 指示[Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2a87f-114">Download and install Azure AD Powershell V2, following hello instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="2a87f-115">下載 Azure AD Utils 模組 hello [azure Ad/azure activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1)。</span><span class="sxs-lookup"><span data-stu-id="2a87f-115">Download hello Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="2a87f-116">此模組會提供數個公用程式 Cmdlet，包括︰</span><span class="sxs-lookup"><span data-stu-id="2a87f-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="2a87f-117">hello 最新版本的 ADAL 使用 Nuget</span><span class="sxs-lookup"><span data-stu-id="2a87f-117">hello latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="2a87f-118">從使用者、應用程式金鑰和憑證存取權杖 (使用 ADAL)</span><span class="sxs-lookup"><span data-stu-id="2a87f-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="2a87f-119">處理分頁結果的圖形 API</span><span class="sxs-lookup"><span data-stu-id="2a87f-119">Graph API handling paged results</span></span>

<span data-ttu-id="2a87f-120">**tooinstall hello Azure AD Utils 模組：**</span><span class="sxs-lookup"><span data-stu-id="2a87f-120">**tooinstall hello Azure AD Utils module:**</span></span>

1. <span data-ttu-id="2a87f-121">建立目錄 toosave hello 公用程式模組 (例如，c:\azureAD)，並從 GitHub 下載 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="2a87f-121">Create a directory toosave hello utilities module (for example, c:\azureAD) and download hello module from GitHub.</span></span>
2. <span data-ttu-id="2a87f-122">開啟的 PowerShell 工作階段，並移 toohello 您剛建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="2a87f-122">Open a PowerShell session, and go toohello directory you just created.</span></span> 
3. <span data-ttu-id="2a87f-123">匯入 hello 模組，並將它安裝在使用 hello 安裝 AzureADUtilsModule cmdlet hello PowerShell 模組路徑。</span><span class="sxs-lookup"><span data-stu-id="2a87f-123">Import hello module, and install it in hello PowerShell module path using hello Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="2a87f-124">hello 工作階段應該看起來類似 toothis 螢幕：</span><span class="sxs-lookup"><span data-stu-id="2a87f-124">hello session should look similar toothis screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a><span data-ttu-id="2a87f-126">設定應用程式中的 hello 憑證</span><span class="sxs-lookup"><span data-stu-id="2a87f-126">Set hello certificate in your app</span></span>
1. <span data-ttu-id="2a87f-127">如果您已經有應用程式，請從 hello Azure 入口網站中取得其物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a87f-127">If you already have an app, get its Object ID from hello Azure Portal.</span></span> 

  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="2a87f-129">開啟 PowerShell 工作階段，並連接 tooAzure AD 使用 hello 連接 azure Ad cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2a87f-129">Open a PowerShell session and connect tooAzure AD using hello Connect-AzureAD cmdlet.</span></span>

  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="2a87f-131">使用從 AzureADUtils tooadd 憑證認證 tooit hello 新增 AzureADApplicationCertificateCredential 指令程式。</span><span class="sxs-lookup"><span data-stu-id="2a87f-131">Use hello New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils tooadd a certificate credential tooit.</span></span> 

>[!Note]
><span data-ttu-id="2a87f-132">您需要 tooprovide hello 應用程式更早版本，而擷取的物件識別碼以及 hello 憑證物件 (此使用 hello Cert： 磁碟機)。</span><span class="sxs-lookup"><span data-stu-id="2a87f-132">You need tooprovide hello application Object ID that you captured earlier, as well as hello certificate object (get this using hello Cert: drive).</span></span>
>


  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="2a87f-134">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="2a87f-134">Get an access token</span></span>

<span data-ttu-id="2a87f-135">tooget 存取權杖，請使用 AzureADUtils hello Get AzureADGraphAPIAccessTokenFromCert cmdlet。</span><span class="sxs-lookup"><span data-stu-id="2a87f-135">tooget an access token, use hello Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="2a87f-136">您需要而不是您在 hello 最後一節中使用的物件識別碼 hello toouse hello 應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="2a87f-136">You need toouse hello Application ID instead of hello Object ID that you used in hello last section.</span></span>
>

 ![Azure 入口網站](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a><span data-ttu-id="2a87f-138">使用 hello 存取語彙基元 toocall hello Graph API</span><span class="sxs-lookup"><span data-stu-id="2a87f-138">Use hello access token toocall hello Graph API</span></span>

<span data-ttu-id="2a87f-139">現在您可以建立 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="2a87f-139">Now you can create hello script.</span></span> <span data-ttu-id="2a87f-140">以下是使用從 hello AzureADUtils hello Invoke AzureADGraphAPIQuery cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="2a87f-140">Below is an example using hello Invoke-AzureADGraphAPIQuery cmdlet from hello AzureADUtils.</span></span> <span data-ttu-id="2a87f-141">此 cmdlet 會處理多個分頁的結果，並接著會傳送這些結果 toohello PowerShell 管線。</span><span class="sxs-lookup"><span data-stu-id="2a87f-141">This cmdlet handles multi-paged results, and then sends those results toohello PowerShell pipeline.</span></span> 

 ![Azure 入口網站](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="2a87f-143">您現在已準備好 tooexport tooa CSV，並儲存 tooa SIEM 系統。</span><span class="sxs-lookup"><span data-stu-id="2a87f-143">You are now ready tooexport tooa CSV and save tooa SIEM system.</span></span> <span data-ttu-id="2a87f-144">您也可以包裝您的指令碼中的排程的工作 tooget Azure AD 資料從您的租用戶定期而不需要在 hello 原始程式碼 toostore 應用程式金鑰。</span><span class="sxs-lookup"><span data-stu-id="2a87f-144">You can also wrap your script in a scheduled task tooget Azure AD data from your tenant periodically without having toostore application keys in hello source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a87f-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a87f-145">Next steps</span></span>
[<span data-ttu-id="2a87f-146">hello Azure 身分識別管理的基本概念</span><span class="sxs-lookup"><span data-stu-id="2a87f-146">hello fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



