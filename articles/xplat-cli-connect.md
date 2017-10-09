---
title: "在從 hello CLI tooAzure aaaLog |Microsoft 文件"
description: "從 hello Azure 命令列介面 (Azure CLI) 連接 tooyour Azure 訂用帳戶，如 Mac、 Linux 及 Windows"
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a>登入從 hello Azure CLI tooAzure
hello Azure CLI 是一組的開放原始碼、 跨平台的命令，以使用 Azure 資源。 本文說明 hello 不同的方式 tooprovide 您的 Azure 帳戶認證 tooconnect hello Azure CLI tooyour Azure 訂用帳戶：

* 執行 hello `azure login` CLI 命令 tooauthenticate 透過 Azure Active Directory。 這個方法可讓您存取 tooCLI 命令，在這兩[命令模式](#cli-command-modes)。 當您執行 hello 命令，而不需要額外的選項，`azure login`會提示您 toocontinue 透過 web 入口網站以互動方式登入。 針對其他`azure login`命令選項，請參閱此文件或類型中的 hello 案例`azure login --help`。
* 如果您只需要 toouse Azure 服務管理模式 CLI 命令 （不建議用於最新的部署），您可以下載並安裝在電腦上的發行設定檔。

如果您尚未安裝 hello CLI，請參閱[安裝 hello Azure CLI](cli-install-nodejs.md)。 如果您沒有 Azure 訂用帳戶，則只需要幾分鐘的時間就可以建立 [免費帳戶](http://azure.microsoft.com/free/) 。

如需不同帳戶身分識別與 Azure 訂用帳戶的背景，請參閱 [Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](active-directory/active-directory-how-subscriptions-associated-directory.md)。

## <a name="scenario-1-azure-login-with-interactive-login"></a>案例 1：使用互動式登入方法來登入 Azure
使用特定的帳戶，hello CLI 需要您 toorun`azure login`然後繼續 hello 登入程序，透過 web 入口網站，稱為程序的網頁瀏覽器*互動式登入*。 常見原因是當您有工作或學校帳戶 (也稱為*組織帳戶*) 設定 toorequire 多重要素驗證。 當您想 toouse 資源管理員模式命令時，也使用與您的 Microsoft 帳戶互動式登入。

互動式登入是簡單： 型別`azure login`-不使用任何選項-hello 下列範例所示：

```
azure login
```                                                                                             

hello 輸出會顯示 hello 下列類似：

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
複製 hello 提供 tooyou hello 命令輸出中的程式碼，並開啟瀏覽器 toohttp://aka.ms/devicelogin 或其他頁面，如果指定。 (您可以開啟瀏覽器上 hello 同一部電腦，或在不同的電腦或裝置上。)輸入 hello 的程式碼，接著便可提示的 tooenter hello 使用者名稱和密碼要 toouse hello 身分識別。 在該程序完成，hello 命令殼層時完成 hello 登入。 會出現類似下面的畫面：

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> 透過互動式登入，驗證和授權都是使用 Azure Active Directory 來執行。 如果您使用 Microsoft 帳戶的身分識別，hello 登入程序會存取您的 Azure Active Directory 預設網域。 (如果您註冊免費 Azure 帳戶，Azure Active Directory 會為您的帳戶自動建立預設網域。)
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a>案例 2：利用使用者名稱和密碼來登入 Azure
使用 hello`azure login`命令與 hello 使用者名稱 (`-u`) 參數 tooauthenticate 時想 toouse 工作或學校帳戶，不需要多重要素驗證。 系統會提示您在 hello 密碼的 hello 命令列 (或者，您可以選擇性地傳遞為 hello 的額外參數的 hello 密碼`azure login`命令)。 hello 下列範例會將 $ hello 的組織帳戶的使用者名稱：

    azure login -u myUserName@contoso.onmicrosoft.com

然後，您會收到提示 tooenter 您的密碼：

    info:    Executing command login
    Password: *********

然後完成 hello 登入程序。

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

如果這是您第一次登入才能執行這些認證時，系統會詢問 tooverify 您希望 toocache 驗證權杖。 如果您先前使用 hello，也會發生此提示`azure logout`命令 （hello 文件中稍後所述）。 toobypass 自動化案例中，這個提示字元執行`azure login`以 hello`-q`參數。

## <a name="scenario-3-azure-login-with-a-service-principal"></a>案例 3：使用服務主體來登入 Azure
如果您建立服務主體的 Active Directory 應用程式，而且 hello 服務主體對您的訂用帳戶的權限，您可以使用 hello`azure login`命令 tooauthenticate hello 服務主體。 根據您的案例中，您可以提供 hello hello 服務主體的認證當做明確參數的 hello`azure login`命令。 例如，hello 下列命令會將 hello 服務主體名稱和 Active Directory 租用戶識別碼：

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

您會再提示的 tooprovide hello 密碼。 您也可以提供 hello 認證透過 CLI 指令碼或應用程式程式碼，或用於自動化案例非互動方式使用憑證 tooauthenticate hello 服務主體。 如需詳細資料與範例，請參閱[使用 Azure Resource Manager 驗證服務主體](resource-group-authenticate-service-principal-cli.md)。

## <a name="scenario-4-use-a-publish-settings-file"></a>案例 4：使用發佈設定檔
如果您只需要 toouse hello Azure 服務管理模式 CLI 命令 (例如，toodeploy Azure Vm 中 hello 傳統部署模型)，您可以使用發行設定檔案連接。 這個方法會將憑證安裝在本機電腦，讓您的 tooperform 管理工作，只要 hello 訂用帳戶和 hello 憑證有效。

* **toodownload hello 的發行設定檔**您的帳戶，請確定 CLI 是服務管理模式中，輸入該 hello `azure config mode asm`。 然後執行下列命令的 hello:

        azure account download

這會開啟預設的瀏覽器，並提示您在 toohello toosign [Azure 傳統入口網站](https://manage.windowsazure.com)。 登入後便會下載 `.publishsettings` 檔案。 請記下此檔案的儲存位置。

> [!NOTE]
> 如果您的帳戶與多個 Azure Active Directory 租用戶相關聯，您可能會是哪一種 Active Directory 想 toodownload 發行設定檔案的提示的 tooselect。
>
>

一旦使用 hello 下載頁面上，選取或瀏覽 hello Azure 傳統入口網站，hello 選取 Active Directory 會變成 hello hello 傳統入口網站並下載頁面使用的預設值。 一旦建立預設值，您會看到 hello 文字 '**按一下這裡 tooreturn toohello 選取 頁面上**' hello 頁面頂端的 hello 下載。 使用 hello 提供連結 tooreturn toohello 選取 頁面。

* **tooimport hello 的發行設定檔**，請執行 hello 下列命令：

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> 匯入之後您將發行設定，您應該刪除 hello`.publishsettings`檔案。 它已不再需要由 hello Azure CLI，並存在安全性風險，因為它可能會使用的 toogain 存取 tooyour 訂用帳戶。
>
>

## <a name="cli-command-modes"></a>CLI 命令模式
hello Azure CLI 提供兩種命令模式使用具有不同的命令集的 Azure 資源：

* **Resource Manager 模式**： 適用於使用 hello Resource Manager 部署模型中的 Azure 資源。 tooset 此模式中，執行`azure config mode arm`。
* **服務管理模式**： 適用於使用 hello 傳統部署模型中的 Azure 資源。 tooset 此模式中，執行`azure config mode asm`。

最初安裝時，hello 的 hello CLI 處於 Resource Manager 模式的目前版本。

> [!NOTE]
> hello Resource Manager 模式和服務管理模式互斥。 也就是一種模式中建立的資源無法在此管理 hello 其他模式。
>
>

## <a name="multiple-subscriptions"></a>多重訂閱
如果您有多個 Azure 訂用帳戶，連接 tooAzure 授與存取您的認證與相關聯的 tooall 訂閱。 一個訂用帳戶是 hello 預設為選取，而且執行作業時，由 hello Azure CLI。 您可以檢視 hello 訂用帳戶，包括 hello 目前預設訂用帳戶，請使用 hello`azure account list`命令。 此命令會傳回類似 toohello 下列資訊：

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

在上述清單中的 hello，hello**目前**資料行會指出 hello 目前預設訂用帳戶與 Azure-sub-1。 toochange hello 預設訂用帳戶，使用 hello`azure account set`命令，然後指定您想 toobe hello 預設 hello 訂用帳戶。 例如：

    azure account set Azure-sub-2

這樣會變更 hello 預設訂用帳戶 tooAzure-sub-2。

> [!NOTE]
> 變更 hello 預設訂用帳戶會立即生效，以及全域變更;新的 Azure CLI 命令，不管您是從執行 hello 相同命令列執行個體或不同的執行個體，使用 hello 新預設訂用帳戶。
>
>

如果您想 toouse hello Azure CLI 的非預設訂用帳戶，但不想 toochange hello 目前的預設值，您可以使用 hello `--subscription` hello 命令選項，然後提供 hello 名稱 hello 訂用帳戶中，您想 toouse hello 作業。

一旦您已連線的 tooyour Azure 訂用帳戶，您可以從開始使用 Azure 資源 hello Azure CLI 命令 toowork。

## <a name="storage-of-cli-settings"></a>CLI 設定的儲存位置
是否登入 hello`azure login`命令或匯入發行設定時，您的 CLI 設定檔和記錄檔儲存在`.azure`目錄位於您`user`目錄。 `user` 目錄已受到作業系統的保護。 不過，我們建議您採取其他步驟 tooencrypt 您`user`目錄。 您可以在 hello 下列方法來這樣做：

* 在 Windows 中，修改 hello 目錄屬性，或使用 BitLocker。
* 在 Mac 上，開啟 FileVault hello 目錄。
* 在 Ubuntu，使用 hello 加密首頁目錄功能。 其他 Linux 散發套件提供類似的功能。

## <a name="logging-out"></a>登出
toolog 出使用 hello 下列命令：

    azure logout -u <username>

如果 hello 訂用帳戶相關聯 hello 帳戶只驗證與 Active Directory，登出 hello 本機設定檔中刪除 hello 訂用帳戶資訊。 不過，如果 hello 訂用帳戶也已匯入發行設定檔，登出只刪除 Active Directory 相關 hello 本機設定檔資訊。

## <a name="next-steps"></a>後續步驟
* toouse Azure CLI 命令，請參閱[Resource Manager 模式中的 Azure CLI 命令](virtual-machines/azure-cli-arm-commands.md)和[服務管理模式中的 Azure CLI 命令](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。
* 深入了解 hello Azure CLI toolearn 下載原始程式碼、 報告的問題，或參與 toohello 專案，請瀏覽 hello [hello Azure CLI 的 GitHub 儲存機制](https://github.com/azure/azure-xplat-cli)。
* 如果您遇到了使用 Azure CLI hello 或 Azure 的問題，請瀏覽 hello [Azure 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting)。
