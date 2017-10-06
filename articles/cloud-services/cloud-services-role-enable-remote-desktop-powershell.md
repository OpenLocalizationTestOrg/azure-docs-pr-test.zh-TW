---
title: "aaaEnable 使用 PowerShell 的 Azure 雲端服務中的角色的遠端桌面連線"
description: "如何 tooconfigure 您的 azure 雲端服務應用程式使用 PowerShell tooallow 遠端桌面連線"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: bf2f70a4-20dc-4302-a91a-38cd7a2baa62
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 3f46b014f29f1c0be0e1b485d2f0152424162bb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services-using-powershell"></a>使用 PowerShell 啟用 Azure 雲端服務中角色的遠端桌面連線
> [!div class="op_single_selector"]
> * [Azure 入口網站](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Azure 傳統入口網站](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

遠端桌面可讓您在 Azure 中執行的角色 tooaccess hello 桌面。 您可以使用遠端桌面連線 tootroubleshoot 後診斷問題的應用程式，在執行時。

本文說明如何使用 PowerShell 將雲端服務角色上的 tooenable 遠端桌面。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) hello 這個發行項所需的必要條件。 PowerShell 會利用 hello 遠端桌面延伸模組，因此您可以在 hello 應用程式部署之後啟用遠端桌面。

## <a name="configure-remote-desktop-from-powershell"></a>從 PowerShell 設定遠端桌面
hello[組 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0)指令程式可讓您指定的角色或您的雲端服務部署的所有角色上 tooenable 遠端桌面。 hello cmdlet 可讓您指定 hello 遠端桌面的使用者透過 hello hello 使用者名稱和密碼*認證*參數可接受 PSCredential 物件。

如果您以互動方式使用 PowerShell，您可以輕鬆地設定 hello PSCredential 物件呼叫 hello[取得認證](https://technet.microsoft.com/library/hh849815.aspx)cmdlet。

```
$remoteusercredentials = Get-Credential
```

此命令會顯示對話方塊，讓您 tooenter hello 使用者名稱和密碼 hello 遠端使用者以安全的方式。

因為 PowerShell 可協助自動化案例中，您也可以設定 hello **PSCredential**物件不需要使用者互動的方式。 首先，您需要 tooset 安全密碼。 您開始使用指定的純文字密碼轉換 tooa 安全字串使用[Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)。 接下來您需要 tooconvert 這個安全字串的加密標準字串使用[Convertfrom-securestring](https://technet.microsoft.com/library/hh849814.aspx)。 現在您可以將儲存此加密標準字串 tooa 檔案使用[Set-content](https://technet.microsoft.com/library/ee176959.aspx)。

您也可以建立安全密碼的檔案，所以您不需要 tootype hello 密碼在每次。 此外，安全的密碼檔案也比純文字檔案安全。 使用下列 PowerShell toocreate 安全密碼檔案的 hello:

```
ConvertTo-SecureString -String "Password123" -AsPlainText -Force | ConvertFrom-SecureString | Set-Content "password.txt"
```

> [!IMPORTANT]
> 當設定 hello 密碼，請確定您符合 hello[複雜性需求](https://technet.microsoft.com/library/cc786468.aspx)。
>
>

從 hello 安全密碼檔案 toocreate hello 認證物件，您必須閱讀 hello 檔案內容並將它們轉換後的 tooa 安全字串使用[Convertto-securestring](https://technet.microsoft.com/library/hh849818.aspx)。

hello[組 AzureServiceRemoteDesktopExtension](/powershell/module/azure/set-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet 也接受*到期*參數，指定**DateTime** hello 使用者帳戶到期。 例如，您可以設定 hello 帳戶 tooexpire 幾天從 hello 目前日期和時間。

此 PowerShell 範例將示範如何 tooset hello 雲端服務上的遠端桌面延伸模組：

```
$servicename = "cloudservice"
$username = "RemoteDesktopUser"
$securepassword = Get-Content -Path "password.txt" | ConvertTo-SecureString
$expiry = $(Get-Date).AddDays(1)
$credential = New-Object System.Management.Automation.PSCredential $username,$securepassword
Set-AzureServiceRemoteDesktopExtension -ServiceName $servicename -Credential $credential -Expiration $expiry
```
您也可以指定 hello 部署位置和要 tooenable 遠端桌面的角色。 如果未指定這些參數，hello cmdlet 可讓 hello 中的所有角色的遠端桌面**生產**部署位置。

hello 遠端桌面延伸模組是與部署相關聯。 如果您建立新的部署的 hello 服務時，您有 tooenable 遠端桌面該部署。 如果您一定想要啟用 toohave 遠端桌面，您應該考慮您的部署工作流程整合 hello PowerShell 指令碼。

## <a name="remote-desktop-into-a-role-instance"></a>從遠端桌面連接到角色執行個體
hello [Get-azureremotedesktopfile](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0)指令程式是使用的 tooremote 桌面連接到您的雲端服務的特定角色執行個體。 您可以使用 hello *LocalPath*參數 toodownload hello RDP 檔案在本機。 您可以使用 hello 或者*啟動*參數 toodirectly 啟動 hello 遠端桌面連線 對話方塊 tooaccess hello 雲端服務角色執行個體。

```
Get-AzureRemoteDesktopFile -ServiceName $servicename -Name "WorkerRole1_IN_0" -Launch
```


## <a name="check-if-remote-desktop-extension-is-enabled-on-a-service"></a>檢查服務上是否已啟用遠端桌面延伸模組
hello [Get AzureServiceRemoteDesktopExtension](/powershell/module/azure/get-azureremotedesktopfile?view=azuresmps-3.7.0) cmdlet 會顯示的遠端桌面已啟用或停用服務部署。 hello cmdlet 會傳回 hello hello 遠端桌面使用者與 hello 角色 hello 遠端桌面延伸模組已啟用的使用者名稱。 根據預設，這發生在 hello 部署位置上，您可以選擇改為暫存位置 toouse hello。

```
Get-AzureServiceRemoteDesktopExtension -ServiceName $servicename
```

## <a name="remove-remote-desktop-extension-from-a-service"></a>從服務移除遠端桌面延伸模組
如果您已啟用 hello 遠端桌面延伸模組的部署，而且需要 tooupdate hello 遠端桌面設定，請先移除 hello 延伸模組。 然後重新啟用的 hello 新設定。 例如，如果您想 tooset hello 遠端使用者帳戶或 hello 帳戶的新密碼過期。 執行此動作需要有 hello 遠端桌面啟用擴充功能的現有部署。 針對新的部署，您只可以直接套用 hello 延伸模組。

tooremove hello 遠端桌面延伸模組從 hello 部署，您可以使用 hello[移除 AzureServiceRemoteDesktopExtension](/powershell/module/azure/remove-azureserviceremotedesktopextension?view=azuresmps-3.7.0) cmdlet。 您也可以選擇指定 hello 部署位置和要從中 tooremove hello 遠端桌面延伸模組的角色。

```
Remove-AzureServiceRemoteDesktopExtension -ServiceName $servicename -UninstallConfiguration
```

> [!NOTE]
> toocompletely 移除 hello 延伸組態，您應該呼叫 hello*移除*cmdlet 搭配 hello **UninstallConfiguration**參數。
>
> hello **UninstallConfiguration**參數解除安裝任何擴充功能組態也就是套用的 toohello 服務。 每個延伸模組組態會與 hello 服務組態關聯。 呼叫 hello*移除*cmdlet 而沒有**UninstallConfiguration**解除關聯 hello<mark>部署</mark>從 hello 延伸組態，因此有效地移除hello 延伸模組。 不過，hello 延伸模組組態會保持與 hello 服務相關聯。
>
>

## <a name="additional-resources"></a>其他資源

[如何 tooConfigure 雲端服務](cloud-services-how-to-configure.md)
[雲端服務的常見問題集-遠端桌面](cloud-services-faq.md)
