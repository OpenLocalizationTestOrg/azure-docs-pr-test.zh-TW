---
title: "aaaPassing 認證使用 DSC tooAzure |Microsoft 文件"
description: "安全地傳遞概觀認證 tooAzure 使用 PowerShell 預期狀態設定的虛擬機器"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a>傳遞認證 toohello Azure DSC 延伸模組處理常式
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

本文涵蓋 Azure hello Desired State Configuration 延伸模組。 Hello DSC 延伸模組處理常式的概觀，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

## <a name="passing-in-credentials"></a>傳入認證
Hello 設定程序的一部分，您可能需要 tooset 使用者帳戶、 存取服務，或安裝程式在使用者內容中。 toodo 情況，您需要 tooprovide 認證。 

DSC 可以參數化設定認證會傳遞至 hello 組態和安全地儲存在 MOF 檔案中。 hello Azure 延伸模組處理常式會提供自動管理的憑證，以簡化認證管理。 

請考慮下列使用 hello 指定的密碼建立本機使用者帳戶的 DSC 設定指令碼的 hello:

*user_configuration.ps1*

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

它是重要的 tooinclude*節點 localhost* hello 組態的一部分。 如果此陳述式遺漏，hello 下列步驟不如 hello 延伸模組處理常式特別會尋找 hello 節點 localhost 陳述式。 很重要，因為 tooinclude hello 類型轉換*[PsCredential]*，如這個特定類型的觸發程序 hello 延伸 tooencrypt hello 認證。 

發行此指令碼 tooblob 存放裝置：

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

設定 hello Azure DSC 延伸模組，並提供 hello 認證：

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a>保護認證的方式
執行此程式碼會提示您輸入認證。 一旦提供認證之後，就會很快地儲存在記憶體中。 當發行與`Set-AzureVmDscExtension`cmdlet，它透過 HTTPS toohello VM 傳輸之後，在 Azure 儲存在磁碟上，使用 hello 本機 VM 憑證加密。 簡短解密和重新加密的 toopass 記憶體，則它 tooDSC。

此行為是不同於[使用安全的設定，而 hello 延伸模組處理常式不](https://msdn.microsoft.com/powershell/dsc/securemof)。 hello Azure 環境可讓您安全地透過憑證的方式 tootransmit 組態資料。 使用 hello DSC 延伸模組處理常式時, 沒有任何需要 tooprovide $CertificatePath 或 $CertificateID / $Thumbprint ConfigurationData 中的項目。

## <a name="next-steps"></a>後續步驟
如需有關 hello Azure DSC 延伸模組處理常式的詳細資訊，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

檢查 hello [hello DSC 延伸模組的 Azure Resource Manager 範本](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。 

toofind 額外的功能，您可以使用 PowerShell DSC[瀏覽 hello PowerShell 資源庫](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0)的多個 DSC 資源。

