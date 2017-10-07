---
title: "aaaConnect tooAzure 堆疊 |Microsoft 文件"
description: "深入了解如何 tooconnect Azure 堆疊"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 3cebbfa6-819a-41e3-9f1b-14ca0a2aaba3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: sngun
ms.openlocfilehash: 8a940245fbcc8795d26b694df66824f0eb1dc3ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-stack"></a>連接 tooAzure 堆疊

toomanage 資源，您必須連接 toohello Azure 堆疊開發套件。 此主題的詳細資料 hello 步驟需要 tooconnect toohello 開發套件。 您可以使用其中一個 hello 下列連接選項：

* [遠端桌面](#connect-with-remote-desktop)： 可讓單一並行使用者快速地連接從 hello 開發套件。
* [虛擬私人網路 (VPN)](#connect-with-vpn)： 可讓多位使用者同時連接從用戶端以外 hello Azure 堆疊基礎結構 （需要組態）。

## <a name="connect-tooazure-stack-with-remote-desktop"></a>使用遠端桌面連線 tooAzure 堆疊
使用遠端桌面連線，hello 入口 toomanage 資源可以處理單一的並行使用者。

1. 開啟 遠端桌面連線並連線 toohello 開發套件。 輸入**AzureStack\AzureStackAdmin** hello 使用者名稱，以及 hello Azure 堆疊安裝過程中提供的系統管理密碼。  

2. 從 hello 開發套件的電腦，開啟伺服器管理員 中，按一下 **本機伺服器**，關閉 Internet Explorer 增強式安全性，，然後再關閉伺服器管理員。

3. tooopen hello 使用者[入口網站](azure-stack-key-features.md#portal)，瀏覽過 (https://portal.local.azurestack.external/) 並使用使用者認證登入。 tooopen hello 管理員[入口網站](azure-stack-key-features.md#portal)，瀏覽過 (https://adminportal.local.azurestack.external/) 和登入使用 hello 在安裝期間指定的 Azure Active Directory 認證。

## <a name="connect-tooazure-stack-with-vpn"></a>使用 VPN 連線 tooAzure 堆疊

您可以建立分割通道虛擬私人網路 (VPN) 連線 tooan Azure 堆疊開發套件。 透過 hello VPN 連線，您可以存取 hello 管理員入口網站，使用者入口網站，及本機上安裝工具，例如 Visual Studio 和 PowerShell toomanage 堆疊 Azure 資源。 Azure Active Directory(AAD) 和「Active Directory 同盟服務」(AD FS) 型部署都支援 VPN 連線。 VPN 連線可讓在 hello 的多個用戶端 tooconnect tooAzure 堆疊相同的時間。 

> [!NOTE] 
> 此 VPN 連線不提供連線 tooAzure 堆疊基礎結構的 Vm。 

### <a name="prerequisites"></a>必要條件

* 在您的本機電腦上安裝 [Azure Stack 相容的 Azure PowerShell](azure-stack-powershell-install.md)。  
* 下載 hello [Azure 堆疊的工具需要的 toowork](azure-stack-powershell-download.md)。 

### <a name="configure-vpn-connectivity"></a>設定 VPN 連線

toocreate VPN 連線 toohello 開發套件，開啟提升權限的 PowerShell 工作階段，從您的本機 Windows 為基礎的電腦和執行下列指令碼 （請確定 tooupdate hello hello IP 位址和密碼值為您的環境） 的 hello:

```PowerShell 
# Configure winrm if it's not already configured
winrm quickconfig  

Set-ExecutionPolicy RemoteSigned

# Import hello Connect module
Import-Module .\Connect\AzureStack.Connect.psm1 

# Add hello development kit computer’s host IP address & certificate authority (CA) toohello list of trusted hosts. Make sure tooupdate hello hello IP address and password values for your environment. 

$hostIP = "<Azure Stack host IP address>"

$Password = ConvertTo-SecureString `
  "<Administrator password provided when deploying Azure Stack>" `
  -AsPlainText `
  -Force

Set-Item wsman:\localhost\Client\TrustedHosts `
  -Value $hostIP `
  -Concatenate

# Create a VPN connection entry for hello local user
Add-AzsVpnConnection `
  -ServerAddress $hostIP `
  -Password $Password

```

如果 hello 設定成功，您應該會看到**azurestack**清單中的 VPN 連線。

![網路連線](media/azure-stack-connect-azure-stack/image3.png)  

### <a name="connect-tooazure-stack"></a>連接 tooAzure 堆疊

使用下列兩種方法的 hello 任一連接 toohello Azure 堆疊的執行個體：  

* 使用 hello`Connect-AzsVpn `命令： 
    
  ```PowerShell
  Connect-AzsVpn `
    -Password $Password
  ```

  出現提示時，信任 hello Azure 堆疊主控件，並安裝來自 hello 憑證**AzureStackCertificateAuthority**到本機電腦憑證存放區。 （hello 提示可能會出現在 hello PowerShell 工作階段視窗後面）。 

* 開啟您本機電腦的 [網路設定] > [VPN] > 按一下 [azurestack] > [連線]。 Hello 登入提示字元之下，輸入 hello 使用者名稱 (AzureStack\AzureStackAdmin) 和 hello 密碼。

### <a name="test-hello-vpn-connectivity"></a>測試 hello VPN 連線能力

tootest hello 入口網站連線，請開啟網際網路瀏覽器和瀏覽 tooeither hello 使用者入口網站 (https://portal.local.azurestack.external/) 或 hello 管理員入口網站 (https://adminportal.local.azurestack.external/)、 登入並建立資源。  

## <a name="next-steps"></a>後續步驟

[讓虛擬機器可用 tooyour Azure 堆疊使用者](azure-stack-tutorial-tenant-vm.md)

