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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>使用 PowerShell 的 Azure App Service SSL 憑證繫結
隨著 Microsoft Azure PowerShell 1.1.0 版的發行，加入了新的 Cmdlet，可讓使用者將現有的或新的 SSL 憑證繫結至現有的 Web 應用程式。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

若要了解如何使用 Azure Resource Manager 架構 Azure PowerShell Cmdlet 來管理您的 Web Apps，請查看 [適用於 Azure Web App 的 Azure Resource Manager 架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>上傳和繫結新的 SSL 憑證
案例：使用者希望將 SSL 憑證繫結至他的其中一個 Web 應用程式。

知道包含 Web 應用程式的資源群組名稱、Web 應用程式名稱、使用者電腦上憑證 .pfx 檔案的路徑、憑證的密碼，以及自訂主機名稱，我們可以使用下列 PowerShell 命令來建立 SSL 繫結：

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

請注意，將 SSL 繫結新增至 Web 應用程式之前，您必須已經設定主機名稱 (自訂網域)。 如果未設定主機名稱，則您在執行 New-AzureRmWebAppSSLBinding 時會收到「主機名稱不存在」錯誤。 您可以直接從入口網站，或使用 Azure PowerShell 新增主機名稱。 下列 PowerShell 程式碼片段可以在執行 New-AzureRmWebAppSSLBinding 之前用來設定主機名稱。   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

請務必了解，Set-AzureRmWebApp Cmdlet 會覆寫 Web 應用程式的主機名稱。 因此，上述 PowerShell 程式碼片段會附加至 Web 應用程式現有的主機名稱清單。  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>上傳和繫結現有的 SSL 憑證
案例：使用者希望將先前上傳的 SSL 憑證繫結至他的其中一個 Web 應用程式。

我們可以使用下列命令來取得已上傳至特定資源群組之憑證的清單

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

請注意，憑證是特定位置和資源群組的本機，如果設定的 Web 應用程式與所需的憑證是在不同的位置和資源群組，使用者必須重新上傳憑證 

知道包含 Web 應用程式的資源群組名稱、Web 應用程式名稱、憑證指紋，以及自訂主機名稱，我們可以使用下列 PowerShell 命令來建立該 SSL 繫結：

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>刪除現有的 SSL 繫結
案例：使用者想要刪除現有的 SSL 繫結。

知道包含 Web 應用程式的資源群組名稱、Web 應用程式名稱，以及自訂主機名稱，我們可以使用下列 PowerShell 命令來移除該 SSL 繫結：

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

請注意，如果移除的 SSL 繫結是在該位置使用該憑證的最後一個繫結，預設將會刪除憑證，而如果使用者想要保留憑證，可以使用 DeleteCertificate 選項來保護憑證

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>參考
* [適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)
* [App Service 環境簡介](app-service-app-service-environment-intro.md)
* [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)

