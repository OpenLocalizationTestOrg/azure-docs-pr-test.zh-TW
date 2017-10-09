---
title: "開始使用 Azure 金鑰保存庫的 aaaGet |Microsoft 文件"
description: "使用您收到本教學課程 toohelp 開始使用 Azure 金鑰保存庫 toocreate 強行寫入的容器在 Azure 中，toostore 和管理密碼編譯金鑰和 Azure 中的密碼。"
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 36721e1d-38b8-4a15-ba6f-14ed5be4de79
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 865853b778dec5fca5c7db0d060627554c0a9cb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-key-vault"></a>開始使用 Azure 金鑰保存庫
大部分地區均提供 Azure 金鑰保存庫。 如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。

## <a name="introduction"></a>簡介
使用您收到本教學課程 toohelp 開始使用 Azure 金鑰保存庫 toocreate 強行寫入的容器 （保存庫） 在 Azure 中，toostore 和管理密碼編譯金鑰和 Azure 中的密碼。 它會引導您透過使用 Azure PowerShell toocreate hello 程序包含金鑰或密碼，您可以使用 Azure 應用程式的保存庫。 接著，它會說明應用程式可以如何使用該金鑰或密碼。

**估計時間 toocomplete:** 20 分鐘

> [!NOTE]
> 本教學課程不包括如何 toowrite hello Azure hello 步驟的其中一個包含的應用程式，也就是如何 tooauthorize 應用程式 toouse 金鑰或密碼中 hello 金鑰保存庫的指示。
>
> 本教學課程使用 Azure PowerShell。 如需跨平台命令列介面的指示，請參閱 [這個對等的教學課程](key-vault-manage-with-cli2.md)。
>
>

如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您必須擁有下列 hello:

* 訂用帳戶 tooMicrosoft Azure。 如果您沒有訂用帳戶，您可以註冊 [免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* Azure PowerShell， **最低版本為 1.1.0**。 tooinstall Azure PowerShell，將它與您 Azure 訂用帳戶產生關聯，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 如果您已安裝 Azure PowerShell，並不知道 hello 版本 hello Azure PowerShell 主控台中，輸入`(Get-Module azure -ListAvailable).Version`。 如果您已安裝 Azure PowerShell 版本 0.9.1 至 0.9.8，您仍可使用本教學課程並稍作變更。 例如，您必須使用 hello`Switch-AzureMode AzureResourceManager`命令以及某些 hello Azure 金鑰保存庫命令已變更。 如需 hello 為 0.9.8 透過 0.9.1 版本的金鑰保存庫 cmdlet 的清單，請參閱[Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。
* 將會設定的 toouse hello 金鑰或密碼，您在本教學課程中建立應用程式。 範例應用程式是可從 hello [Microsoft Download Center](http://www.microsoft.com/en-us/download/details.aspx?id=45343)。 如需指示，請參閱 hello 隨附的讀我檔案。

此教學課程的設計為 Azure PowerShell 初學者所設計，但它假設您已了解 hello 基本概念，例如模組、 cmdlet 和工作階段。 如需詳細資訊，請參閱 [開始使用 Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)。

tooget 詳細說明您在此教學課程中，使用 hello 中看到任何 cmdlet **Get-help** cmdlet。

    Get-Help <cmdlet-name> -Detailed

例如，tooget 說明 hello**登入 AzureRmAccount** cmdlet，類型：

    Get-Help Login-AzureRmAccount -Detailed

您也可以閱讀下列教學課程 tooget 熟悉與 Azure 資源管理員的 Azure PowerShell hello:

* [如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell 搭配資源管理員使用](../powershell-azure-resource-manager.md)

## <a id="connect"></a>連接 tooyour 訂用帳戶
啟動 Azure PowerShell 工作階段，以登入 Azure 帳戶 tooyour hello 下列命令：  

    Login-AzureRmAccount

請注意，如果您使用 Azure 中，例如 Azure 政府的特定執行個體使用 hello-使用此命令的環境參數。 例如：`Login-AzureRmAccount –Environment (Get-AzureRmEnvironment –Name AzureUSGovernment)`

在 [hello] 快顯瀏覽器視窗中，輸入您的 Azure 帳戶使用者名稱和密碼。 Azure PowerShell 取得所有 hello 訂用帳戶相關聯，與此帳戶，而且依預設，會使用 hello 第一個。

如果您有多個訂用帳戶，並想 toospecify 特定一個 toouse for Azure Key Vault，輸入下列帳戶 toosee hello 訂閱 hello:

    Get-AzureRmSubscription

然後，toospecify hello 訂用帳戶 toouse，類型：

    Set-AzureRmContext -SubscriptionId <subscription ID>

如需有關如何設定 Azure PowerShell 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

## <a id="resource"></a>建立新的資源群組
使用 Azure 資源管理員時，會在資源群組中建立所有相關資源。 在本教學課程中，我們將建立名為 **ContosoResourceGroup** 的新資源群組：

    New-AzureRmResourceGroup –Name 'ContosoResourceGroup' –Location 'East Asia'


## <a id="vault"></a>建立金鑰保存庫
使用 hello[新增 AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) cmdlet toocreate 金鑰保存庫。 這個 cmdlet 包含三個必要參數：**資源群組名稱**、**金鑰保存庫名稱**，和 hello**地理位置**。

例如，如果您使用保存庫名稱 hello **ContosoKeyVault**，hello 資源群組名稱**ContosoResourceGroup**，和 hello 位置**東亞**，類型：

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia'

此 cmdlet 的 hello 輸出會顯示您剛才建立的 hello 金鑰保存庫的內容。 hello 兩個最重要的屬性包括：

* **保存庫名稱**: hello 範例中，這是**ContosoKeyVault**。 您將在其他金鑰保存庫 Cmdlet 中使用此名稱。
* **保存庫 URI**: hello 範例中，這是 https://contosokeyvault.vault.azure.net/。 透過其 REST API 使用保存庫的應用程式必須使用此 URI。

現在已授權的 tooperform 保存庫上此金鑰的任何作業，就會是您的 Azure 帳戶。 而且，沒有其他人有此授權。

> [!NOTE]
> 如果您看到 hello 錯誤**hello 訂用帳戶未註冊的 toouse 命名空間 'Microsoft.KeyVault'**當您嘗試 toocreate 新金鑰保存庫，執行`Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"`，然後重新執行新增 AzureRmKeyVault 命令。 如需詳細資訊，請參閱 [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider)。
>
>

## <a id="add"></a>新增金鑰或密碼 toohello 金鑰保存庫
如果您想為您的 Azure 金鑰保存庫 toocreate 受軟體保護的金鑰，請使用 hello [Add-azurekeyvaultkey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet，然後輸入 hello 下列：

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -Destination 'Software'

不過，如果您在現有受軟體保護金鑰。PFX 檔案儲存 tooyour C:\ 磁碟機中名為您想 tooupload tooAzure 金鑰保存庫，遵循 tooset hello 變數的型別 hello softkey.pfx **securepfxpwd**密碼**123** hello。PFX 檔案：

    $securepfxpwd = ConvertTo-SecureString –String '123' –AsPlainText –Force

然後輸入 hello hello 中的下列 tooimport hello 索引鍵。PFX 檔案，它會透過 hello 金鑰保存庫服務中的軟體保護金鑰 hello:

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd


您現在可以參考此機碼，您建立或上傳 tooAzure 金鑰保存庫中，使用它的 URI。 使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways 取得 hello 目前的版本，並使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget 這個特定的版本。  

此索引鍵，類型 toodisplay hello URI:

    $Key.key.kid

tooadd 秘密 toohello 保存庫，這是名為 SQLPassword 密碼，且擁有 hello 值 Pa$ $w0rd tooAzure 金鑰保存庫，將第一次 Pa$ $w0rd tooa 安全字串 hello 值輸入 hello 下列轉換：

    $secretvalue = ConvertTo-SecureString 'Pa$$w0rd' -AsPlainText -Force

然後輸入 hello 下列：

    $secret = Set-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword' -SecretValue $secretvalue

您現在可以參考您藉由使用其 URI 新增 tooAzure 金鑰保存庫，此密碼。 使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways 取得 hello 目前的版本，並使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget 這個特定的版本。

此密碼，類型為 toodisplay hello URI:

    $secret.Id

讓我們來檢視 hello 金鑰或您剛才建立的密碼：

* tooview 您索引鍵，類型：`Get-AzureKeyVaultKey –VaultName 'ContosoKeyVault'`
* tooview 秘密，型別：`Get-AzureKeyVaultSecret –VaultName 'ContosoKeyVault'`

現在，您的金鑰保存庫和金鑰或密碼已準備好應用程式 toouse。 您必須授權應用程式 toouse 它們。  

## <a id="register"></a>向 Azure Active Directory 註冊應用程式
這步驟通常會由開發人員在個別電腦上完成。 它不是特定 tooAzure 金鑰保存庫，但是仍然包含在此處為求完整起見。

> [!IMPORTANT]
> toocomplete hello 教學課程，您的帳戶、 hello 保存庫和您要登錄在此步驟中的 hello 應用程式都必須在 hello 相同的 Azure 目錄。
>
>

使用金鑰保存庫的應用程式必須使用 Azure Active Directory 的權杖進行驗證。 toodo，hello hello 應用程式的擁有者必須先註冊他們的 Azure Active Directory 中的 hello 應用程式。 在 hello 註冊結尾，hello 應用程式擁有者取得 hello 下列值：

* **應用程式識別碼**(也稱為用戶端 ID) 和**驗證金鑰**（也稱為 hello 共用的密碼）。 hello 應用程式必須提供這兩個這些值 tooAzure Active Directory、 tooget 語彙基元。 Hello 應用程式的方式設定的 toodo 這取決於 hello 應用程式。 Hello 金鑰保存庫的範例應用程式，hello 應用程式擁有者，請 hello app.config 檔案中設定這些值。

在 Azure Active Directory tooregister hello 應用程式：

1. 登入 toohello Azure 傳統入口網站。
2. Hello 左側，按一下  **Active Directory**，然後選取您要在其中登錄您的應用程式的 hello 目錄。 <br> <br> **注意：**您必須選取 hello 含有相同目錄 hello 您用來建立金鑰保存庫的 Azure 訂用帳戶。 如果您不知道哪個目錄這是，按一下 **設定**，識別 hello 訂閱您用來建立金鑰保存庫，並注意 hello hello 目錄名稱顯示 hello 最後一個資料行。
3. 按一下 [ **應用程式**]。 如果沒有任何應用程式已加入 tooyour 目錄，此頁面會顯示只有 hello**新增應用程式**連結。 按一下 [hello] 連結，或或者，您可以按一下**新增**hello 命令列上。
4. 在 hello**新增應用程式**精靈，在 hello**您該怎麼想 toodo？**頁面上，按一下**加入我組織正在開發的應用程式**。
5. 在 hello**告訴我們您的應用程式**頁面上，指定您的應用程式的名稱，然後選取**WEB 應用程式和/或 WEB API** (hello 預設值)。 按一下 hello**下一步**圖示。
6. 在 hello**應用程式屬性**頁面上，指定 hello**登入 URL**和**應用程式識別碼 URI** web 應用程式。 如果您的應用程式沒有這些值，您可以在此步驟中虛構這些值 (例如，您可以在這兩個方塊中指定 http://test1.contoso.com)。 這些網站是否存在並不重要。 重要的是每個應用程式的 hello 應用程式識別碼 URI 是不同的目錄中的每個應用程式。 hello 目錄會使用此字串 tooidentify 您的應用程式。
7. 按一下 hello**完成**圖示 toosave hello 精靈中的變更。
8. 在 hello**快速入門**頁面上，按一下**設定**。
9. 捲動 toohello**金鑰**區段中選取 hello 持續時間，然後再按一下**儲存**。 hello 頁面重新整理，而且現在會顯示金鑰值。 您必須設定您的應用程式具有此機碼值與 hello**用戶端識別碼**值。 (有關此設定的指示僅適用於特定應用程式。)
10. 複製此頁面上，您會在您的保存庫使用 hello 下一個步驟 tooset 權限中的 hello 用戶端識別碼值。

## <a id="authorize"></a>授權 hello 應用程式 toouse hello 金鑰或密碼
tooauthorize hello 應用程式 tooaccess hello hello 保存庫，使用中金鑰或密碼[Set-azurermkeyvaultaccesspolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet。

例如，如果您的保存庫名稱是**ContosoKeyVault**和您想 tooauthorize 具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed，用戶端識別碼，而且您想 tooauthorize hello 應用程式 toodecrypt 並登入索引鍵中的 hello 應用程式您的保存庫，執行下列 hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get

## <a id="HSM"></a>如果您想 toouse 硬體安全性模組 (HSM)
為求保險，您可以匯入，或在硬體安全性模組 (Hsm)，絕不能離開 hello HSM 界限中產生的索引鍵。 hello Hsm 是的 FIPS 140-2 Level 2 驗證。 如果這項需求不適 tooyou，略過本節並移太[刪除 hello 金鑰保存庫及相關聯的金鑰和秘密](#delete)。

toocreate 這些受 HSM 保護的金鑰，您必須使用 hello [Azure 金鑰保存庫 Premium 服務層 toosupport 受 HSM 保護金鑰](https://azure.microsoft.com/pricing/free-trial/)。 此外，請注意此功能不適用於 Azure China。

當您建立 hello 金鑰保存庫時，新增 hello **-SKU**參數：

    New-AzureRmKeyVault -VaultName 'ContosoKeyVaultHSM' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -SKU 'Premium'



您可以將軟體保護金鑰 （如下所示稍早） 和 HSM 保護的金鑰 toothis 金鑰保存庫。 toocreate HSM 保護的金鑰組 hello **-目的地**參數 too'HSM':

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -Destination 'HSM'

您可以使用下列命令 tooimport hello 的金鑰。在您的電腦上的 PFX 檔案。 這個命令匯入 hello 金鑰 Hsm hello 金鑰保存庫服務中：

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\softkey.pfx' -KeyFilePassword $securepfxpwd -Destination 'HSM'


hello 下一個命令會匯入 「 攜帶您自己的金鑰 」 (BYOK) 封裝。 此案例可讓您在您本機的 HSM 中產生您的金鑰並將金鑰傳輸 tooHSMs hello 金鑰保存庫服務中的不需要離開 hello HSM 界限的 hello 金鑰：

    $key = Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMKey' -KeyFilePath 'c:\ITByok.byok' -Destination 'HSM'

如需詳細說明 toogenerate 這個 BYOK 封裝，請參閱[如何為 Azure 金鑰保存庫的 toogenerate 並傳輸受 HSM 保護金鑰](key-vault-hsm-protected-keys.md)。

## <a id="delete"></a>刪除 hello 金鑰保存庫及相關聯的金鑰和密碼
如果您不再需要 hello 金鑰保存庫和 hello 金鑰或密碼，其中的內容，您可以刪除 hello 金鑰保存庫使用 hello[移除 AzureRmKeyVault](/powershell/module/azurerm.keyvault/remove-azurermkeyvault) cmdlet:

    Remove-AzureRmKeyVault -VaultName 'ContosoKeyVault'

或者，您可以刪除整個 Azure 資源群組，其中包括 hello 金鑰保存庫和您在該群組中包含的任何其他資源：

    Remove-AzureRmResourceGroup -ResourceGroupName 'ContosoResourceGroup'


## <a id="other"></a>其他 Azure PowerShell Cmdlet
可能有助於管理 Azure 金鑰保存庫的其他命令：

* `$Keys = Get-AzureKeyVaultKey -VaultName 'ContosoKeyVault'`此命令會取得以表格形式顯示的所有金鑰和所選屬性。
* `$Keys[0]`： 這個命令會顯示完整的 hello 指定索引鍵的屬性清單
* `Get-AzureKeyVaultSecret`此命令會列出以表格形式顯示的所有密碼名稱和所選屬性。
* `Remove-AzureKeyVaultKey -VaultName 'ContosoKeyVault' -Name 'ContosoFirstKey'`： 範例如何 tooremove 特定索引鍵。
* `Remove-AzureKeyVaultSecret -VaultName 'ContosoKeyVault' -Name 'SQLPassword'`： 範例如何 tooremove 特定密碼。

## <a id="next"></a>接續步驟
如需在 Web 應用程式中使用 Azure 金鑰保存庫的後續教學課程，請參閱 [從 Web 應用程式使用 Azure 金鑰保存庫](key-vault-use-from-web-application.md)。

toosee 如何使用金鑰保存庫，請參閱[Azure 金鑰保存庫記錄](key-vault-logging.md)。

如需 hello Azure 金鑰保存庫的最新版 Azure PowerShell cmdlet 的清單，請參閱[Azure Key Vault Cmdlet](/powershell/module/azurerm.keyvault/#key_vault)。

程式設計參考，請參閱[hello Azure 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。
