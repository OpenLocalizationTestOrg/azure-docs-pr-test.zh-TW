---
title: "aaaSSL 憑證繫結使用 PowerShell"
description: "了解如何 toobind SSL 憑證使用 PowerShell tooyour web 應用程式。"
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 8ce32508-e982-48d3-b878-0e526afda537
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: 82f0e7c796da99ab50f69f3638ef64d55a94fc8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="8002f-103">使用 PowerShell 的 Azure App Service SSL 憑證繫結</span><span class="sxs-lookup"><span data-stu-id="8002f-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="8002f-104">Hello 版本的 Microsoft Azure PowerShell 1.1.0 版已加入新的 cmdlet，這樣會使 hello 使用者 hello 能力 toobind 現有或新 SSL 憑證 tooan 現有 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8002f-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give hello user hello ability toobind existing or new SSL certificates tooan existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="8002f-105">有關使用 Azure Resource Manager toolearn 基礎的 Azure PowerShell cmdlet toomanage 您 Web 應用程式的簽入[Azure 資源管理員的 Azure Web 應用程式架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8002f-105">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="8002f-106">上傳和繫結新的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="8002f-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="8002f-107">案例： hello 使用者希望 toobind 他的 web 應用程式的 SSL 憑證 tooone。</span><span class="sxs-lookup"><span data-stu-id="8002f-107">Scenario: hello user would like toobind an SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="8002f-108">了解 hello 資源群組名稱包含 hello web 應用程式、 hello web 應用程式名稱、 hello hello 使用者在電腦上，憑證.pfx 檔案路徑 hello hello 憑證密碼 hello 自訂主機名稱，我們可以使用下列 PowerShell 命令 toocreate hello，SSL 繫結：</span><span class="sxs-lookup"><span data-stu-id="8002f-108">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate .pfx file path on hello user machine, hello password for hello certificate, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="8002f-109">請注意，然後再加入 SSL 繫結 tooa web 應用程式，您必須擁有已設定的主機名稱 （自訂的網域）。</span><span class="sxs-lookup"><span data-stu-id="8002f-109">Note that before adding a SSL binding tooa web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="8002f-110">如果未設定 hello 主機名稱，則您會收到錯誤時執行新增 AzureRmWebAppSSLBinding 'hostname' 不存在。</span><span class="sxs-lookup"><span data-stu-id="8002f-110">If hello host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="8002f-111">您可以直接從 hello 入口網站或使用 Azure PowerShell 新增的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8002f-111">You can add a hostname directly from hello portal or using Azure PowerShell.</span></span> <span data-ttu-id="8002f-112">hello 下列 PowerShell 程式碼片段 tooconfigure hello 主機名稱之前可執行新增 AzureRmWebAppSSLBinding。</span><span class="sxs-lookup"><span data-stu-id="8002f-112">hello following PowerShell snippet can be tooconfigure hello hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="8002f-113">請務必 hello 組 AzureRmWebApp cmdlet 的 toounderstand 會覆寫 hello hello web 應用程式的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="8002f-113">It is important toounderstand that hello Set-AzureRmWebApp cmdlet overwrites hello hostnames for hello web app.</span></span> <span data-ttu-id="8002f-114">因此 hello 上述 PowerShell 程式碼片段會附加 toohello 的 hello hello web 應用程式的主機名稱的現有清單。</span><span class="sxs-lookup"><span data-stu-id="8002f-114">Hence hello above PowerShell snippet is appending toohello existing list of hello host names for hello web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="8002f-115">上傳和繫結現有的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="8002f-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="8002f-116">案例： hello 使用者希望 toobind 先前上傳 SSL 憑證 tooone 他的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8002f-116">Scenario: hello user would like toobind a previously uploaded SSL certificate tooone of his web apps.</span></span>

<span data-ttu-id="8002f-117">我們可以得到 hello 清單的憑證已上傳的 tooa 特定資源群組使用下列命令的 hello</span><span class="sxs-lookup"><span data-stu-id="8002f-117">We can get hello list of certificates already uploaded tooa specific resource group by using hello following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="8002f-118">請注意，hello 憑證是本機 tooa 特定位置和資源群組，hello 使用者需要 toore 上載 hello 憑證如果 hello 設定 web 應用程式是在不同的位置與資源群組的需要憑證的 hello</span><span class="sxs-lookup"><span data-stu-id="8002f-118">Note that hello certificates are local tooa specific location and resource group, hello user need toore-upload hello certificate if hello configured web app is in a different location and resource group other that that of hello needed certificate</span></span> 

<span data-ttu-id="8002f-119">了解 hello 資源群組名稱，其中包含 hello web 應用程式，hello web 應用程式名稱、 hello 憑證指紋和 hello 自訂主機名稱，請我們可以使用下列 PowerShell 命令 toocreate hello 的 SSL 繫結：</span><span class="sxs-lookup"><span data-stu-id="8002f-119">Knowing hello resource group name that contains hello web app, hello web app name, hello certificate thumbprint, and hello custom hostname, we can use hello following PowerShell command toocreate that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="8002f-120">刪除現有的 SSL 繫結</span><span class="sxs-lookup"><span data-stu-id="8002f-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="8002f-121">案例： hello 使用者希望 toodelete 現有的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="8002f-121">Scenario: hello user would like toodelete an existing SSL binding.</span></span>

<span data-ttu-id="8002f-122">了解 hello 資源群組名稱，其中包含 hello web 應用程式，hello web 應用程式名稱，和 hello 自訂主機名稱，我們可以使用下列 PowerShell 命令 tooremove hello SSL 繫結的：</span><span class="sxs-lookup"><span data-stu-id="8002f-122">Knowing hello resource group name that contains hello web app, hello web app name, and hello custom hostname, we can use hello following PowerShell command tooremove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="8002f-123">請注意，如果 hello 移除 SSL 繫結已 hello 上次在該位置中，使用該憑證繫結的預設 hello 憑證將被刪除，如果 hello 使用者想 tookeep hello 憑證他可以使用 hello DeleteCertificate 選項 tookeep hello 憑證</span><span class="sxs-lookup"><span data-stu-id="8002f-123">Note that if hello removed SSL binding was hello last binding using that certificate in that location, by default hello certificate will be deleted, if hello user want tookeep hello certificate he can use hello DeleteCertificate option tookeep hello certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="8002f-124">參考</span><span class="sxs-lookup"><span data-stu-id="8002f-124">References</span></span>
* [<span data-ttu-id="8002f-125">適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="8002f-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="8002f-126">簡介 tooApp Service 環境</span><span class="sxs-lookup"><span data-stu-id="8002f-126">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="8002f-127">搭配使用 Azure PowerShell 與 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="8002f-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

