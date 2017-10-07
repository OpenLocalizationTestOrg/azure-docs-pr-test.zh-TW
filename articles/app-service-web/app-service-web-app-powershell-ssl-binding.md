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
# <a name="azure-app-service-ssl-certificate-binding-using-powershell"></a>使用 PowerShell 的 Azure App Service SSL 憑證繫結
Hello 版本的 Microsoft Azure PowerShell 1.1.0 版已加入新的 cmdlet，這樣會使 hello 使用者 hello 能力 toobind 現有或新 SSL 憑證 tooan 現有 Web 應用程式。

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

有關使用 Azure Resource Manager toolearn 基礎的 Azure PowerShell cmdlet toomanage 您 Web 應用程式的簽入[Azure 資源管理員的 Azure Web 應用程式架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="uploading-and-binding-a-new-ssl-certificate"></a>上傳和繫結新的 SSL 憑證
案例： hello 使用者希望 toobind 他的 web 應用程式的 SSL 憑證 tooone。

了解 hello 資源群組名稱包含 hello web 應用程式、 hello web 應用程式名稱、 hello hello 使用者在電腦上，憑證.pfx 檔案路徑 hello hello 憑證密碼 hello 自訂主機名稱，我們可以使用下列 PowerShell 命令 toocreate hello，SSL 繫結：

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -CertificateFilePath PathToPfxFile -CertificatePassword PlainTextPwd -Name www.contoso.com

請注意，然後再加入 SSL 繫結 tooa web 應用程式，您必須擁有已設定的主機名稱 （自訂的網域）。 如果未設定 hello 主機名稱，則您會收到錯誤時執行新增 AzureRmWebAppSSLBinding 'hostname' 不存在。 您可以直接從 hello 入口網站或使用 Azure PowerShell 新增的主機名稱。 hello 下列 PowerShell 程式碼片段 tooconfigure hello 主機名稱之前可執行新增 AzureRmWebAppSSLBinding。   

    $webApp = Get-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup  
    $hostNames = $webApp.HostNames  
    $HostNames.Add("www.contoso.com")  
    Set-AzureRmWebApp -Name mytestapp -ResourceGroupName myresourcegroup -HostNames $HostNames   

請務必 hello 組 AzureRmWebApp cmdlet 的 toounderstand 會覆寫 hello hello web 應用程式的主機名稱。 因此 hello 上述 PowerShell 程式碼片段會附加 toohello 的 hello hello web 應用程式的主機名稱的現有清單。  

## <a name="uploading-and-binding-an-existing-ssl-certificate"></a>上傳和繫結現有的 SSL 憑證
案例： hello 使用者希望 toobind 先前上傳 SSL 憑證 tooone 他的 web 應用程式。

我們可以得到 hello 清單的憑證已上傳的 tooa 特定資源群組使用下列命令的 hello

    Get-AzureRmWebAppCertificate -ResourceGroupName myresourcegroup

請注意，hello 憑證是本機 tooa 特定位置和資源群組，hello 使用者需要 toore 上載 hello 憑證如果 hello 設定 web 應用程式是在不同的位置與資源群組的需要憑證的 hello 

了解 hello 資源群組名稱，其中包含 hello web 應用程式，hello web 應用程式名稱、 hello 憑證指紋和 hello 自訂主機名稱，請我們可以使用下列 PowerShell 命令 toocreate hello 的 SSL 繫結：

    New-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Thumbprint <certificate thumbprint> -Name www.contoso.com

## <a name="deleting-an-existing-ssl-binding"></a>刪除現有的 SSL 繫結
案例： hello 使用者希望 toodelete 現有的 SSL 繫結。

了解 hello 資源群組名稱，其中包含 hello web 應用程式，hello web 應用程式名稱，和 hello 自訂主機名稱，我們可以使用下列 PowerShell 命令 tooremove hello SSL 繫結的：

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com

請注意，如果 hello 移除 SSL 繫結已 hello 上次在該位置中，使用該憑證繫結的預設 hello 憑證將被刪除，如果 hello 使用者想 tookeep hello 憑證他可以使用 hello DeleteCertificate 選項 tookeep hello 憑證

    Remove-AzureRmWebAppSSLBinding -ResourceGroupName myresourcegroup -WebAppName mytestapp -Name www.contoso.com -DeleteCertificate $false

### <a name="references"></a>參考
* [適用於 Azure Web 應用程式的 Azure Resource Manager 架構 PowerShell 命令](app-service-web-app-azure-resource-manager-powershell.md)
* [簡介 tooApp Service 環境](app-service-app-service-environment-intro.md)
* [搭配使用 Azure PowerShell 與 Azure 資源管理員](../powershell-azure-resource-manager.md)

