---
title: "使用 Azure AD 報告 API 搭配憑證來取得資料 | Microsoft Docs"
description: "說明如何使用 Azure AD 報告 API 搭配憑證認證來取得目錄中的資料，而不需使用者介入。"
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
ms.openlocfilehash: c1345dcda6e52267a8037ffd7207e6bc3b0d3b31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="get-data-using-the-azure-ad-reporting-api-with-certificates"></a><span data-ttu-id="3b8ec-103">使用 Azure AD 報告 API 搭配憑證來取得資料</span><span class="sxs-lookup"><span data-stu-id="3b8ec-103">Get data using the Azure AD Reporting API with certificates</span></span>
<span data-ttu-id="3b8ec-104">本文討論如何使用 Azure AD 報告 API 搭配憑證認證來取得目錄中的資料，而不需使用者介入。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-104">This article discusses how to use the Azure AD Reporting API with certificate credentials to get data from directories without user intervention.</span></span> 

## <a name="use-the-azure-ad-reporting-api"></a><span data-ttu-id="3b8ec-105">使用 Azure AD 報告 API</span><span class="sxs-lookup"><span data-stu-id="3b8ec-105">Use the Azure AD Reporting API</span></span> 
<span data-ttu-id="3b8ec-106">Azure AD Reporting API 會要求您完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="3b8ec-106">Azure AD Reporting API requires that you complete the following steps:</span></span>
 *  <span data-ttu-id="3b8ec-107">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="3b8ec-107">Install prerequisites</span></span>
 *  <span data-ttu-id="3b8ec-108">在您的應用程式中設定憑證</span><span class="sxs-lookup"><span data-stu-id="3b8ec-108">Set the certificate in your app</span></span>
 *  <span data-ttu-id="3b8ec-109">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="3b8ec-109">Get an access token</span></span>
 *  <span data-ttu-id="3b8ec-110">使用存取權杖來呼叫圖形 API</span><span class="sxs-lookup"><span data-stu-id="3b8ec-110">Use the access token to call the Graph API</span></span>

<span data-ttu-id="3b8ec-111">如需原始程式碼的相關資訊，請參閱[運用報告 API 模組](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils)。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-111">For information about source code, see [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils).</span></span> 

### <a name="install-prerequisites"></a><span data-ttu-id="3b8ec-112">安裝必要條件</span><span class="sxs-lookup"><span data-stu-id="3b8ec-112">Install prerequisites</span></span>
<span data-ttu-id="3b8ec-113">您必須已安裝 Azure AD PowerShell V2 和 AzureADUtils 模組。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-113">You will need to have Azure AD PowerShell V2 and AzureADUtils module installed.</span></span>

1. <span data-ttu-id="3b8ec-114">遵循 [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md) 的指示，下載並安裝 Azure AD Powershell V2。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-114">Download and install Azure AD Powershell V2, following the instructions at [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).</span></span>
2. <span data-ttu-id="3b8ec-115">從 [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1) 下載 Azure AD Utils 模組。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-115">Download the Azure AD Utils module from [AzureAD/azure-activedirectory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1).</span></span> 
  <span data-ttu-id="3b8ec-116">此模組會提供數個公用程式 Cmdlet，包括︰</span><span class="sxs-lookup"><span data-stu-id="3b8ec-116">This module provides several utility cmdlets including:</span></span>
   * <span data-ttu-id="3b8ec-117">最新版的 ADAL (使用 Nuget)</span><span class="sxs-lookup"><span data-stu-id="3b8ec-117">The latest version of ADAL using Nuget</span></span>
   * <span data-ttu-id="3b8ec-118">從使用者、應用程式金鑰和憑證存取權杖 (使用 ADAL)</span><span class="sxs-lookup"><span data-stu-id="3b8ec-118">Access tokens from user, application keys, and certificates using ADAL</span></span>
   * <span data-ttu-id="3b8ec-119">處理分頁結果的圖形 API</span><span class="sxs-lookup"><span data-stu-id="3b8ec-119">Graph API handling paged results</span></span>

<span data-ttu-id="3b8ec-120">**若要安裝 Azure AD Utils 模組：**</span><span class="sxs-lookup"><span data-stu-id="3b8ec-120">**To install the Azure AD Utils module:**</span></span>

1. <span data-ttu-id="3b8ec-121">建立目錄來儲存公用程式模組 (例如 c:\azureAD) 並從 GitHub 下載此模組。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-121">Create a directory to save the utilities module (for example, c:\azureAD) and download the module from GitHub.</span></span>
2. <span data-ttu-id="3b8ec-122">開啟 PowerShell 工作階段，然後移至您剛建立的目錄。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-122">Open a PowerShell session, and go to the directory you just created.</span></span> 
3. <span data-ttu-id="3b8ec-123">匯入模組，並使用 Install-AzureADUtilsModule Cmdlet 將它安裝於 PowerShell 模組路徑中。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-123">Import the module, and install it in the PowerShell module path using the Install-AzureADUtilsModule cmdlet.</span></span> 

<span data-ttu-id="3b8ec-124">此工作階段看起來應類似這個畫面：</span><span class="sxs-lookup"><span data-stu-id="3b8ec-124">The session should look similar to this screen:</span></span>

  ![Windows Powershell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-the-certificate-in-your-app"></a><span data-ttu-id="3b8ec-126">在您的應用程式中設定憑證</span><span class="sxs-lookup"><span data-stu-id="3b8ec-126">Set the certificate in your app</span></span>
1. <span data-ttu-id="3b8ec-127">如果您已經有應用程式，請從 Azure 入口網站取得其物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-127">If you already have an app, get its Object ID from the Azure Portal.</span></span> 

  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. <span data-ttu-id="3b8ec-129">開啟 PowerShell 工作階段並使用 Connect-AzureAD Cmdlet 連線至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-129">Open a PowerShell session and connect to Azure AD using the Connect-AzureAD cmdlet.</span></span>

  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. <span data-ttu-id="3b8ec-131">使用 AzureADUtils 中的 New-AzureADApplicationCertificateCredential Cmdlet，將憑證認證新增至該模組。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-131">Use the New-AzureADApplicationCertificateCredential cmdlet from AzureADUtils to add a certificate credential to it.</span></span> 

>[!Note]
><span data-ttu-id="3b8ec-132">您必須提供先前擷取的應用程式物件識別碼，以及憑證物件 (使用 Cert: 磁碟機取得此物件)。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-132">You need to provide the application Object ID that you captured earlier, as well as the certificate object (get this using the Cert: drive).</span></span>
>


  ![Azure 入口網站](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a><span data-ttu-id="3b8ec-134">取得存取權杖</span><span class="sxs-lookup"><span data-stu-id="3b8ec-134">Get an access token</span></span>

<span data-ttu-id="3b8ec-135">若要取得存取權杖，請使用 AzureADUtils 中的 Get-AzureADGraphAPIAccessTokenFromCert Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-135">To get an access token, use the Get-AzureADGraphAPIAccessTokenFromCert cmdlet from AzureADUtils.</span></span> 

>[!NOTE]
><span data-ttu-id="3b8ec-136">您必須使用應用程式識別碼，而不是您在上一節中使用的物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-136">You need to use the Application ID instead of the Object ID that you used in the last section.</span></span>
>

 ![Azure 入口網站](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-the-access-token-to-call-the-graph-api"></a><span data-ttu-id="3b8ec-138">使用存取權杖來呼叫圖形 API</span><span class="sxs-lookup"><span data-stu-id="3b8ec-138">Use the access token to call the Graph API</span></span>

<span data-ttu-id="3b8ec-139">您現在可以建立指令碼。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-139">Now you can create the script.</span></span> <span data-ttu-id="3b8ec-140">以下是使用 AzureADUtils 中 Invoke-AzureADGraphAPIQuery Cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-140">Below is an example using the Invoke-AzureADGraphAPIQuery cmdlet from the AzureADUtils.</span></span> <span data-ttu-id="3b8ec-141">這個 Cmdlet 可處理多個分頁結果，然後再將這些結果傳送至 PowerShell 管線。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-141">This cmdlet handles multi-paged results, and then sends those results to the PowerShell pipeline.</span></span> 

 ![Azure 入口網站](./media/active-directory-report-api-with-certificates/script-completed.png)

<span data-ttu-id="3b8ec-143">您現在已準備好匯出至 CSV 並儲存至 SIEM 系統。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-143">You are now ready to export to a CSV and save to a SIEM system.</span></span> <span data-ttu-id="3b8ec-144">您也可以在排定的工作中包裝您的指令碼，以便定期從租用戶取得 Azure AD 資料，而不必將應用程式金鑰儲存在原始程式碼中。</span><span class="sxs-lookup"><span data-stu-id="3b8ec-144">You can also wrap your script in a scheduled task to get Azure AD data from your tenant periodically without having to store application keys in the source code.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3b8ec-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b8ec-145">Next steps</span></span>
[<span data-ttu-id="3b8ec-146">Azure 身分識別管理的基本概念</span><span class="sxs-lookup"><span data-stu-id="3b8ec-146">The fundamentals of Azure identity management</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



