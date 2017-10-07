---
title: aaaDownload hello Azure SDK for PHP
description: "了解如何 toodownload 並安裝 hello Azure SDK for PHP。"
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a>下載 hello Azure SDK for PHP
## <a name="overview"></a>概觀
hello Azure SDK for PHP 包含 toodevelop 可讓您的元件、 部署和管理 Azure 的 PHP 應用程式。 具體來說，hello Azure SDK for PHP 包含 hello 下列：

* **Azure 的 hello PHP 用戶端程式庫**。 這些類別庫所提供的介面可供存取 Azure 功能，例如資料管理服務和雲端服務。  
* **hello Mac、 Linux 及 Windows (Azure CLI) 的 Azure 命令列介面**。 這是一組命令，可用於部署和管理 Azure 服務，例如 Azure 網站和 Azure 虛擬機器。 hello Azure CLI 任何平台，包括 Mac、 Linux 及 Windows 上的工作。
* **Azure PowerShell (僅限 Windows)**。 這是一組 PowerShell Cmdlet，可用於部署和管理 Azure 服務，例如雲端服務和虛擬機器。
* **hello （僅限 Windows） Azure 模擬器**。 hello 計算和儲存體模擬器是雲端服務和資料管理服務可讓您 tootest 本機應用程式的本機模擬器。 hello Azure 模擬器上執行 Windows 只。

hello 下列各節說明 toodownload 並安裝 hello 上面所述的元件。

hello 本主題中的指示假設您有[PHP] [ install-php]安裝。

> [!NOTE]
> 適用於 Azure，您必須擁有 PHP 5.5 或更新版本 toouse hello PHP 用戶端程式庫。
> 
> 

## <a name="php-client-libraries-for-azure"></a>適用於 Azure 的 PHP 用戶端程式庫
Azure 的 hello PHP 用戶端程式庫提供介面來存取 Azure 的功能，例如資料管理服務和雲端服務，從任何作業系統。 可以透過 hello 編輯器安裝這些程式庫。

如需如何 toouse hello azure 的 PHP 用戶端程式庫的資訊，請參閱[tooUse hello Blob 服務的方式][blob-service]， [tooUse hello 表格服務的方式][ table-service]和[tooUse hello 佇列服務的方式][queue-service]。

### <a name="install-via-composer"></a>透過編輯器安裝
1. [安裝 Git][install-git]。

    > [AZURE.NOTE] 在 Windows 中，您也需要 tooadd hello Git 可執行檔 tooyour PATH 環境變數。

1. 建立名為**composer.json**在 hello 您專案的根目錄，並加入下列程式碼 tooit hello:
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. 將 **[composer.phar][composer-phar]** 下載到專案根目錄中。
3. 開啟命令提示字元，在專案根目錄中執行此命令
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell 和 Azure 模擬器
Azure PowerShell 是一組 PowerShell Cmdlet，可用於部署和管理 Azure 服務 (例如雲端服務和虛擬機器)。 hello Azure 模擬器是雲端服務和資料管理服務可讓您 tootest 本機應用程式的模擬器。 只有 Windows 支援這些元件。

hello 建議 tooinstall Azure PowerShell 和 hello Azure 模擬器為 toouse hello [Microsoft Web Platform Installer][download-wpi]。 請注意，您也可以選擇 tooinstall 其他開發元件，例如 PHP、 SQL Server、 hello Microsoft Drivers for PHP 和 WebMatrix 的 SQL Server。

如需有關資訊 toouse Azure PowerShell，請參閱[如何 tooUse Azure PowerShell][powershell-tools]。

## <a name="azure-cli"></a>Azure CLI
hello Azure CLI 是一組命令用來部署和管理 Azure 服務，例如 Azure 網站和 Azure 虛擬機器。 如需安裝 Azure CLI 資訊，請參閱[安裝 hello Azure CLI](cli-install-nodejs.md)。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [PHP 開發人員中心](/develop/php/)。

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
