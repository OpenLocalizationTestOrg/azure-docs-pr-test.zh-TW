---
title: "使用 PowerShell 的 SSL 憑證繫結"
description: "了解如何使用 PowerShell 將 SSL 憑證繫結至您的 Web 應用程式。"
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
ms.openlocfilehash: a1fcc618fb0c68778e39cc227368a60b008f9401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a><span data-ttu-id="296bb-103">使用 PowerShell 的 Azure App Service SSL 憑證繫結</span><span class="sxs-lookup"><span data-stu-id="296bb-103">Azure App Service SSL Certificate Binding using PowerShell</span></span>
<span data-ttu-id="296bb-104">隨著 Microsoft Azure PowerShell 1.1.0 版的發行，加入了新的 Cmdlet，可讓使用者將現有的或新的 SSL 憑證繫結至現有的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="296bb-104">With the release of Microsoft Azure PowerShell version 1.1.0 a new cmdlet has been added that would give the user the ability to bind existing or new SSL certificates to an existing Web App.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="296bb-105">若要了解如何使用 Azure Resource Manager 架構 Azure PowerShell Cmdlet 來管理您的 Web Apps，請查看 [適用於 Azure Web App 的 Azure Resource Manager 架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="296bb-105">To learn about using Azure Resource Manager based Azure PowerShell cmdlets to manage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="uploading-and-binding-a-new-ssl-certificate"></a><span data-ttu-id="296bb-106">上傳和繫結新的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="296bb-106">Uploading and Binding a new SSL certificate</span></span>
<span data-ttu-id="296bb-107">案例：使用者希望將 SSL 憑證繫結至他的其中一個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="296bb-107">Scenario: The user would like to bind an SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="296bb-108">知道包含 Web 應用程式的資源群組名稱、Web 應用程式名稱、使用者電腦上憑證 .pfx 檔案的路徑、憑證的密碼，以及自訂主機名稱，我們可以使用下列 PowerShell 命令來建立 SSL 繫結：</span><span class="sxs-lookup"><span data-stu-id="296bb-108">Knowing the resource group name that contains the web app, the web app name, the certificate .pfx file path on the user machine, the password for the certificate, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

<span data-ttu-id="296bb-109">請注意，將 SSL 繫結新增至 Web 應用程式之前，您必須已經設定主機名稱 (自訂網域)。</span><span class="sxs-lookup"><span data-stu-id="296bb-109">Note that before adding a SSL binding to a web app, you must have a host name (custom domain) already configured.</span></span> <span data-ttu-id="296bb-110">如果未設定主機名稱，則您在執行 New-AzureRmWebAppSSLBinding 時會收到「主機名稱不存在」錯誤。</span><span class="sxs-lookup"><span data-stu-id="296bb-110">If the host name is not configured , then you will get an error 'hostname' does not exist while running  New-AzureRmWebAppSSLBinding.</span></span> <span data-ttu-id="296bb-111">您可以直接從入口網站，或使用 Azure PowerShell 新增主機名稱。</span><span class="sxs-lookup"><span data-stu-id="296bb-111">You can add a hostname directly from the portal or using Azure PowerShell.</span></span> <span data-ttu-id="296bb-112">下列 PowerShell 程式碼片段可以在執行 New-AzureRmWebAppSSLBinding 之前用來設定主機名稱。</span><span class="sxs-lookup"><span data-stu-id="296bb-112">The following PowerShell snippet can be to configure the hostname before running New-AzureRmWebAppSSLBinding.</span></span>   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

<span data-ttu-id="296bb-113">請務必了解，Set-AzureRmWebApp Cmdlet 會覆寫 Web 應用程式的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="296bb-113">It is important to understand that the Set-AzureRmWebApp cmdlet overwrites the hostnames for the web app.</span></span> <span data-ttu-id="296bb-114">因此，上述 PowerShell 程式碼片段會附加至 Web 應用程式現有的主機名稱清單。</span><span class="sxs-lookup"><span data-stu-id="296bb-114">Hence the above PowerShell snippet is appending to the existing list of the host names for the web app.</span></span>  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a><span data-ttu-id="296bb-115">上傳和繫結現有的 SSL 憑證</span><span class="sxs-lookup"><span data-stu-id="296bb-115">Uploading and Binding an existing SSL certificate</span></span>
<span data-ttu-id="296bb-116">案例：使用者希望將先前上傳的 SSL 憑證繫結至他的其中一個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="296bb-116">Scenario: The user would like to bind a previously uploaded SSL certificate to one of his web apps.</span></span>

<span data-ttu-id="296bb-117">我們可以使用下列命令來取得已上傳至特定資源群組之憑證的清單</span><span class="sxs-lookup"><span data-stu-id="296bb-117">We can get the list of certificates already uploaded to a specific resource group by using the following command</span></span>

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

<span data-ttu-id="296bb-118">請注意，憑證是特定位置和資源群組的本機，如果設定的 Web 應用程式與所需的憑證是在不同的位置和資源群組，使用者必須重新上傳憑證</span><span class="sxs-lookup"><span data-stu-id="296bb-118">Note that the certificates are local to a specific location and resource group, the user need to re-upload the certificate if the configured web app is in a different location and resource group other that that of the needed certificate</span></span> 

<span data-ttu-id="296bb-119">知道包含 Web 應用程式的資源群組名稱、Web 應用程式名稱、憑證指紋，以及自訂主機名稱，我們可以使用下列 PowerShell 命令來建立該 SSL 繫結：</span><span class="sxs-lookup"><span data-stu-id="296bb-119">Knowing the resource group name that contains the web app, the web app name, the certificate thumbprint, and the custom hostname, we can use the following PowerShell command to create that SSL binding:</span></span>

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a><span data-ttu-id="296bb-120">刪除現有的 SSL 繫結</span><span class="sxs-lookup"><span data-stu-id="296bb-120">Deleting an existing SSL binding</span></span>
<span data-ttu-id="296bb-121">案例：使用者想要刪除現有的 SSL 繫結。</span><span class="sxs-lookup"><span data-stu-id="296bb-121">Scenario: The user would like to delete an existing SSL binding.</span></span>

<span data-ttu-id="296bb-122">知道包含 Web 應用程式的資源群組名稱、Web 應用程式名稱，以及自訂主機名稱，我們可以使用下列 PowerShell 命令來移除該 SSL 繫結：</span><span class="sxs-lookup"><span data-stu-id="296bb-122">Knowing the resource group name that contains the web app, the web app name, and the custom hostname, we can use the following PowerShell command to remove that SSL binding:</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

<span data-ttu-id="296bb-123">請注意，如果移除的 SSL 繫結是在該位置使用該憑證的最後一個繫結，預設將會刪除憑證，而如果使用者想要保留憑證，可以使用 DeleteCertificate 選項來保護憑證</span><span class="sxs-lookup"><span data-stu-id="296bb-123">Note that if the removed SSL binding was the last binding using that certificate in that location, by default the certificate will be deleted, if the user want to keep the certificate he can use the DeleteCertificate option to keep the certificate</span></span>

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a><span data-ttu-id="296bb-124">參考</span><span class="sxs-lookup"><span data-stu-id="296bb-124">References</span></span>
* [<span data-ttu-id="296bb-125">適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令</span><span class="sxs-lookup"><span data-stu-id="296bb-125">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="296bb-126">App Service 環境簡介</span><span class="sxs-lookup"><span data-stu-id="296bb-126">Introduction to App Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="296bb-127">搭配使用 Azure PowerShell 與 Azure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="296bb-127">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

