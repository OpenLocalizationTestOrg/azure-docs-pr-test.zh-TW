---
title: "Azure 金鑰保存庫使用 CLI aaaManage |Microsoft 文件"
description: "金鑰保存庫中使用此教學課程 tooautomate 一般工作，使用 hello CLI"
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: 9ef506faa67e1f0db5b9e303300d63b135ddd7b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli"></a>使用 CLI 管理金鑰保存庫

大部分地區均提供 Azure 金鑰保存庫。 如需詳細資訊，請參閱 hello[金鑰保存庫定價頁面](https://azure.microsoft.com/pricing/details/key-vault/)。

## <a name="introduction"></a>簡介

使用您收到本教學課程 toohelp 開始使用 Azure 金鑰保存庫 toocreate 強行寫入的容器 （保存庫） 在 Azure 中，toostore 和管理密碼編譯金鑰和 Azure 中的密碼。 它會引導您透過使用 Azure 跨平台命令列介面 toocreate hello 程序包含金鑰或密碼，您可以使用 Azure 應用程式的保存庫。 接著，它會說明應用程式後續可以如何使用該金鑰或密碼。

**估計時間 toocomplete:** 20 分鐘

> [!NOTE]
> 本教學課程不包括指示 toowrite hello Azure 應用程式的其中一個 hello 步驟包含時，會顯示如何 tooauthorize 應用程式 toouse 索引鍵或 hello 機碼中的密碼保存庫的方式。
> 
> 目前，您無法在 hello Azure 入口網站中設定 Azure 金鑰保存庫。 請改用這些跨平台命令列介面指示。 或者，如需 Azure PowerShell 的指示，請參閱 [這個對等的教學課程](key-vault-get-started.md)。
> 
> 

如需 Azure 金鑰保存庫的概觀資訊，請參閱 [什麼是 Azure 金鑰保存庫？](key-vault-whatis.md)

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您必須擁有下列 hello:

* 訂用帳戶 tooMicrosoft Azure。 如果您沒有訂用帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial)。
* 命令列介面 0.9.1 版或更新版本。 tooinstall hello 最新版本，並連接 tooyour Azure 訂用帳戶，請參閱[安裝及設定 Azure 跨平台命令列介面 hello](../cli-install-nodejs.md)。
* 將會設定的 toouse hello 金鑰或密碼，您在本教學課程中建立應用程式。 範例應用程式是可從 hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343)。 如需指示，請參閱 hello 隨附的讀我檔案。

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>取得使用 Azure 跨平台命令列介面的說明

本教學課程假設您熟悉 hello 命令列介面 （Bash，終端機，命令提示字元）

hello-說明或-h 參數可以是 tooview 說明用於特定的命令。 或者，azure 的 hello 說明 [命令] [選項] 格式也可以使用的 tooreturn hello 相同的資訊。 比方說，hello 下列命令傳回所有 hello 相同的資訊：

    azure account set --help

    azure account set -h

    azure help account set

關於 hello 參數所需的命令有疑問，請參閱使用 toohelp-說明、-h 或 azure 說明 [命令]。

您也可以閱讀下列教學課程 tooget 熟悉使用 Azure Resource Manager Azure 跨平台命令列介面中的 hello:

* [如何 tooinstall 及設定 Azure 跨平台命令列介面](../cli-install-nodejs.md)
* [搭配 Azure 資源管理員使用 Azure 跨平台命令列介面](../xplat-cli-azure-resource-manager.md)

## <a name="connect-tooyour-subscriptions"></a>連接 tooyour 訂用帳戶

在使用組織帳戶，下列命令使用 hello toolog:

    azure login -u username -p password

或如果您希望 toolog 以互動方式輸入

    azure login

> [!NOTE]
> hello 登入方法只適用於組織帳戶。 組織帳戶是您組織所管理的使用者，且定義於組織的 Azure Active Directory 租用戶中。
> 
> 

如果您目前沒有組織帳戶，並使用 Microsoft 帳戶 toolog tooyour Azure 訂用帳戶中，您可以輕鬆地建立一個使用下列步驟 hello。

1. 登入 toohello 登入 toohello [Azure 管理入口網站](https://manage.windowsazure.com/)，然後按一下 Active Directory。
2. 如果目錄不存在，請選取 建立您的目錄並提供 hello 要求的資訊。
3. 選取您的目錄並新增使用者。 這個新使用者即為組織帳戶。 Hello 建立期間 hello 使用者，您會提供與 hello 使用者的電子郵件地址和暫時密碼。 請儲存此資訊，其他步驟中將會使用該資訊。
4. 從 hello 入口網站中，選取設定，然後選取系統管理員。 選取 [新增]，並將 hello 新使用者加入為共同管理員。 這可讓 hello 組織帳戶 toomanage 您 Azure 訂用帳戶。
5. 最後，登出 hello Azure 入口網站後再重新登入使用 hello 新的組織帳戶。 如果這是 hello 以這個帳戶的第一個時間登入，您將會提示的 toochange hello 密碼。

如需關於搭配 Microsoft Azure 使用組織帳戶的詳細資訊，請參閱 [以組織身分註冊 Microsoft Azure](../active-directory/sign-up-organization.md)。

如果您有多個訂用帳戶，並想 toospecify 特定一個 toouse for Azure Key Vault，輸入下列帳戶 toosee hello 訂閱 hello:

    azure account list

然後，toospecify hello 訂用帳戶 toouse，類型：

    azure account set <subscription name>

如需有關如何設定 Azure 跨平台命令列介面的詳細資訊，請參閱[如何 tooInstall 和設定 Azure 跨平台命令列介面](../cli-install-nodejs.md)。

## <a name="switch-toousing-azure-resource-manager"></a>切換 toousing Azure 資源管理員
hello 金鑰保存庫，您需要 Azure 資源管理員，因此請輸入 hello 遵循 tooswitch tooAzure Resource Manager 模式：

    azure config mode arm

## <a name="create-a-new-resource-group"></a>建立新的資源群組
使用 Azure 資源管理員時，會在資源群組內建立所有相關資源。 在本教學課程中，我們將建立新的資源群組 'ContosoResourceGroup'。

    azure group create 'ContosoResourceGroup' 'East Asia'

hello 第一個參數是資源群組名稱，且 hello 第二個參數是 hello 的位置。 位置，請使用 hello 命令`azure location list`tooidentify 如何 toospecify 替代位置 toohello 其中一個在此範例中。 如果您需要更多資訊，請輸入： `azure help location`

## <a name="register-hello-key-vault-resource-provider"></a>註冊 hello 金鑰保存庫資源提供者
請確定已在訂用帳戶中註冊金鑰保存庫資源提供者：

`azure provider register Microsoft.KeyVault`

這個動作只需要執行一次，每個訂閱的 toobe。

## <a name="create-a-key-vault"></a>建立金鑰保存庫

使用 hello`azure keyvault create`命令 toocreate 金鑰保存庫。 此指令碼有三個必要參數： 資源群組名稱、 金鑰保存庫名稱和 hello 地理位置。

例如，如果您使用 ContosoKeyVault ContosoResourceGroup，hello 資源群組名稱和東亞、 hello 位置 hello 保存庫名稱輸入：

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

hello 輸出此命令會顯示您剛才建立的 hello 金鑰保存庫的內容。 hello 兩個最重要的屬性包括：

* **名稱**: hello 範例中，這是 ContosoKeyVault。 您將在其他金鑰保存庫 Cmdlet 中使用此名稱。
* **vaultUri**: hello 範例中，這是 https://contosokeyvault.vault.azure.net。 透過其 REST API 使用保存庫的應用程式必須使用此 URI。

現在已授權的 tooperform 保存庫上此金鑰的任何作業，就會是您的 Azure 帳戶。 而且，沒有其他人有此授權。

## <a name="add-a-key-or-secret-toohello-key-vault"></a>新增金鑰或密碼 toohello 金鑰保存庫

如果您想為您的 Azure 金鑰保存庫 toocreate 受軟體保護的金鑰，請使用 hello`azure key create`命令，然後輸入 hello 下列：

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

不過，如果您有現有的索引鍵.pem 檔案，以本機檔案儲存在名為 softkey.pem 想 tooupload tooAzure 金鑰保存庫的檔案中，輸入 hello hello 中的下列 tooimport hello 索引鍵。PEM 檔案，它會透過 hello 金鑰保存庫服務中的軟體保護金鑰 hello:

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

您現在可以參考 hello 金鑰，您建立或上傳 tooAzure 金鑰保存庫中，使用它的 URI。 使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways 取得 hello 目前的版本，並使用**https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget 這個特定的版本。

tooadd 秘密 toohello 保存庫，這是名為 SQLPassword 密碼，並且 hello 值的 Pa$ $w0rd tooAzure 金鑰保存庫中，下列類型 hello:

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

您現在可以參考您藉由使用其 URI 新增 tooAzure 金鑰保存庫，此密碼。 使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways 取得 hello 目前的版本，並使用**https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget 這個特定的版本。

讓我們來檢視 hello 金鑰或您剛才建立的密碼：

* tooview 您索引鍵，類型：`azure keyvault key list --vault-name 'ContosoKeyVault'`
* tooview 秘密，型別：`azure keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>向 Azure Active Directory 註冊應用程式

這步驟通常會由開發人員在個別電腦上完成。 它不是特定 tooAzure 金鑰保存庫，但隨附在這裡，以求完整。

> [!IMPORTANT]
> toocomplete hello 教學課程，您的帳戶、 hello 保存庫和您要登錄在此步驟中的 hello 應用程式都必須在 hello 相同的 Azure 目錄。
> 
> 

使用金鑰保存庫的應用程式必須使用 Azure Active Directory 的權杖進行驗證。 toodo，hello hello 應用程式的擁有者必須先註冊他們的 Azure Active Directory 中的 hello 應用程式。 在 hello 註冊結尾，hello 應用程式擁有者取得 hello 下列值：

* **應用程式識別碼**(也稱為用戶端 ID) 和**驗證金鑰**（也稱為 hello 共用的密碼）。 hello 應用程式必須提供這兩個這些值 tooAzure Active Directory，tooget 語彙基元。 Hello 應用程式的方式設定的 toodo 這取決於 hello 應用程式。 Hello 金鑰保存庫的範例應用程式，hello 應用程式擁有者，請 hello app.config 檔案中設定這些值。

在 Azure Active Directory tooregister hello 應用程式：

1. 登入 toohello Azure 入口網站。
2. Hello 左側，按一下  **Active Directory**，然後選取您要在其中登錄您的應用程式的 hello 目錄。 <br> <br> 

>[!NOTE] 
> 您必須選取 hello 含有相同目錄 hello 您用來建立金鑰保存庫的 Azure 訂用帳戶。 如果您不知道哪個目錄這是，按一下 **設定**，識別 hello 訂閱您用來建立金鑰保存庫，並注意 hello hello 目錄名稱顯示 hello 最後一個資料行。

3. 按一下 [ **應用程式**]。 如果沒有任何應用程式已加入 tooyour 目錄，此頁面會顯示只有 hello**新增應用程式**連結。 按一下 [hello] 連結，或或者，您可以按一下 hello**新增**hello 命令列上。
4. 在 hello**新增應用程式**精靈，在 hello**您該怎麼想 toodo？**頁面上，按一下**加入我組織正在開發的應用程式**。
5. 在 hello**告訴我們您的應用程式**頁面上，指定您的應用程式的名稱，然後選取**WEB 應用程式和/或 WEB API** (hello 預設值)。 按一下 [下一步 hello] 圖示。
6. 在 hello**應用程式屬性**頁面上，指定 hello**登入 URL**和**應用程式識別碼 URI** web 應用程式。 如果您的應用程式沒有這些值，您可以在此步驟中虛構這些值 (例如，您可以在這兩個方塊中指定 http://test1.contoso.com)。 並不重要如果存在這些站台。重要的是每個應用程式的 hello 應用程式識別碼 URI 是不同的目錄中的每個應用程式。 hello 目錄會使用此字串 tooidentify 您的應用程式。
7. 按一下 hello 完成圖示 toosave hello 精靈中的變更。
8. 在 hello 快速入門 頁面上，按一下 **設定**。
9. 捲動 toohello**金鑰**區段中選取 hello 持續時間，然後再按一下**儲存**。 hello 頁面重新整理，而且現在會顯示金鑰值。 您必須設定您的應用程式具有此機碼值與 hello**用戶端識別碼**值。 (有關此設定的指示僅適用於特定應用程式。)
10. 複製此頁面上，您會在您的保存庫使用 hello 下一個步驟 tooset 權限中的 hello 用戶端識別碼值。

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>授權 hello 應用程式 toouse hello 金鑰或密碼
tooauthorize hello 應用程式 tooaccess hello 金鑰或密碼在 hello 保存庫使用 hello`azure keyvault set-policy`命令。

例如，如果您想 tooauthorize 具有 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed，用戶端識別碼，而且您想 tooauthorize hello 應用程式 toodecrypt 並登入具有索引鍵在您的保存庫中的 ContosoKeyVault 和 hello 應用程式保存庫名稱，然後執行 hello下列：

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> 如果您在 Windows 命令提示字元上執行，您應該取代單引號與雙引號，並也逸出 hello 內部雙引號括住。 例如："[\"decrypt\",\"sign\"]"。
> 
> 

如果您想 tooauthorize 該相同的應用程式 tooread 密碼在您的保存庫中，執行下列 hello:

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>如果您想 toouse 硬體安全性模組 (HSM)
為求保險，您可以匯入，或在硬體安全性模組 (Hsm)，絕不能離開 hello HSM 界限中產生的索引鍵。 hello Hsm 是的 FIPS 140-2 Level 2 驗證。 如果這項需求不適 tooyou，略過本節並移太[刪除 hello 金鑰保存庫及相關聯的金鑰和秘密](#delete-the-key-vault-and-associated-keys-and-secrets)。

toocreate 這些受 HSM 保護的金鑰，您必須擁有支援 HSM 保護的金鑰保存庫訂用帳戶。

當您建立 hello keyvault 時，加入 hello 'sku' 參數：

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

您可以將軟體保護的金鑰 （如稍早所示） 和 toothis 受 HSM 保護的金鑰保存庫。 toocreate HSM 保護的金鑰組 hello 目的地參數 too'HSM':

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

您可以使用 hello.pem 檔案，儲存在電腦中的下列命令 tooimport 索引鍵。 這個命令匯入 hello 金鑰 Hsm hello 金鑰保存庫服務中：

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

hello 下一個命令會匯入 「 攜帶您自己的金鑰 」 (BYOK) 封裝。 這可讓您在您本機的 HSM 中產生您的金鑰並將金鑰傳輸 tooHSMs hello 金鑰保存庫服務中的不需要離開 hello HSM 界限的 hello 金鑰：

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

如需詳細說明 toogenerate 這個 BYOK 封裝，請參閱[如何 toouse HSM-Protected 索引鍵，使用 Azure Key Vault](key-vault-hsm-protected-keys.md)。

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>刪除 hello 金鑰保存庫及相關聯的金鑰和密碼
如果您不再需要 hello 金鑰保存庫和 hello 金鑰或密碼，其中的內容，您可以使用 azure 的 hello keyvault delete 命令來刪除 hello 金鑰保存庫：

    azure keyvault delete --vault-name 'ContosoKeyVault'

或者，您可以刪除整個 Azure 資源群組，其中包括 hello 金鑰保存庫和您在該群組中包含的任何其他資源：

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a>其他 Azure 跨平台命令列介面命令
可能有助於管理 Azure 金鑰保存庫的其他命令。

此命令會列出以表格形式顯示的所有金鑰和所選屬性：

    azure keyvault key list --vault-name 'ContosoKeyVault'

此命令會顯示 hello 指定索引鍵屬性的完整清單：

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

此命令會列出以表格形式顯示的所有密碼名稱和所選屬性：

    azure keyvault secret list --vault-name 'ContosoKeyVault'

以下是如何的範例 tooremove 特定索引鍵：

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

以下是如何的範例 tooremove 特定密碼：

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a>後續步驟
程式設計參考，請參閱[hello Azure 金鑰保存庫開發人員手冊 》](key-vault-developers-guide.md)。

