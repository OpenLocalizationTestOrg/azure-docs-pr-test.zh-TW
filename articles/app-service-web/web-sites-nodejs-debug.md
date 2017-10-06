---
title: "aaaHow toodebug Node.js web 應用程式在 Azure 應用程式服務"
description: "了解如何 toodebug Node.js web 應用程式在 Azure App Service 中。"
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Toodebug Node.js web 應用程式在 Azure App Service 中的方式
Azure 提供內建的診斷與偵錯 Node.js 應用程式中裝載的 tooassist [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式。 在本文中，您將學習如何 tooenable 記錄 stdout 和 stderr、 在 hello 瀏覽器中顯示錯誤資訊和 toodownload 和檢視記錄檔。

對於 Azure 上裝載的 Node.js 應用程式，診斷程式由 [IISNode]提供。 雖然這篇文章討論 hello 最常見的設定用於蒐集診斷資訊，它不使用 IISNode 提供完整的參考。 如需使用 IISNode 的詳細資訊，請參閱 hello [IISNode 讀我檔案]GitHub 上。

<a id="enablelogging"></a>

## <a name="enable-logging"></a>啟用記錄
依預設，App Service Web 應用程式只擷取關於部署的診斷資訊，例如使用 Git 來部署 Web 應用程式時。 如果您在部署時發生問題，此資訊很有用，例如安裝 **package.json**中參考的模組失敗時，或使用自訂部署指令碼時。

tooenable hello stdout 和 stderr 資料流的記錄，您必須建立**IISNode.yml**根目錄 hello Node.js 應用程式檔案，然後加入下列 hello:

    loggingEnabled: true

這可讓 hello 記錄 stderr 和 stdout 從 Node.js 應用程式。

hello **IISNode.yml**檔案也可以使用的 toocontrol 是否易懂的錯誤訊息或開發人員錯誤傳回 toohello 瀏覽器發生失敗時。 tooenable 開發人員錯誤，加入下列行 toohello hello **IISNode.yml**檔案：

    devErrorsEnabled: true

一旦啟用此選項，IISNode 會傳回 hello 最後 64k 傳送 toostderr 而不是易記的錯誤，例如 「 發生內部伺服器錯誤 」 的資訊。

> [!NOTE]
> 雖然 devErrorsEnabled 在開發期間在診斷問題時很有用，讓它在生產環境中可能會導致傳送 tooend 使用者開發錯誤。
> 
> 

如果 hello **IISNode.yml**檔案原本不存在您的應用程式內、 發行 hello 更新應用程式之後必須重新啟動您的 web 應用程式。 如果只是在先前發行的現有 **IISNode.yml** 檔案中變更設定，則不需要重新啟動。

> [!NOTE]
> 如果您的 web 應用程式使用 hello Azure 命令列工具或 Azure PowerShell Cmdlet，預設值建立**IISNode.yml**會自動建立檔案。
> 
> 

toorestart hello web 應用程式中，選取 hello web 應用程式在 hello [Azure 入口網站](https://portal.azure.com)，然後按一下**重新啟動**按鈕：

![restart button][restart-button]

如果 hello Azure 命令列工具安裝在開發環境中，您可以使用下列命令 toorestart hello web 應用程式的 hello:

    azure site restart [sitename]

> [!NOTE]
> 雖然 loggingEnabled 和 devErrorsEnabled 擷取診斷資訊的最常用的 hello IISNode.yml 組態選項，IISNode.yml 可以使用的 tooconfigure 各種裝載環境的選項。 如需 hello 組態選項的完整清單，請參閱 hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml)檔案。
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>存取記錄檔
三種方式; 可以存取診斷記錄檔使用 hello 檔案傳輸通訊協定 (FTP)，下載 Zip 封存，或做為即時更新的 hello 記錄 （也稱為結尾） 的資料流。 下載 hello Zip 封存的 hello 記錄檔，或檢視 hello 即時資料流需要 hello Azure 命令列工具。 這些可以使用下列命令的 hello 安裝：

    npm install azure-cli -g

安裝之後，就可以使用 hello 'azure' 命令來存取 hello 工具。 hello 命令列工具必須先設定的 toouse 您 Azure 訂用帳戶。 如需如何 tooaccomplish 這工作資訊，請參閱 hello **toodownload 和匯入發行設定**區段 hello [tooUse hello Azure 命令列工具的方式](../xplat-cli-connect.md)發行項。

### <a name="ftp"></a>FTP
透過 FTP，tooaccess hello 診斷資訊，請瀏覽 hello [Azure 入口網站](https://portal.azure.com)，選取您的 web 應用程式，然後選取 hello**儀表板**。 在 hello**快速連結**區段，hello **FTP 診斷記錄**和**FTPS 診斷記錄**連結提供使用 hello FTP 通訊協定存取 toohello 記錄檔。

> [!NOTE]
> 如果您先前未設定使用者名稱和密碼的 FTP 或部署，您可以從 hello**快速入門**管理頁面中的選取**設定部署認證**。
> 
> 

hello 傳回 hello 儀表板中的 FTP URL 為 hello **LogFiles**目錄，將會包含下列子目錄的 hello:

* [部署方法](web-sites-deploy.md)-如果您使用的部署方法，例如 Git，hello 相同名稱將會建立，而且會包含資訊的目錄相關 toodeployments。
* nodejs - 從應用程式的所有執行個體擷取的 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。

### <a name="zip-archive"></a>Zip 封存檔
toodownload Zip 封存 hello 診斷記錄檔的使用 hello hello Azure 命令列工具中的下列命令：

    azure site log download [sitename]

這會下載**diagnostics.zip** hello 目前目錄中。 這個封存包含下列目錄結構的 hello:

* deployments - 關於應用程式部署的資訊記錄
* LogFiles
  
  * [部署方法](web-sites-deploy.md)-如果您使用的部署方法，例如 Git，hello 相同名稱將會建立，而且會包含資訊的目錄相關 toodeployments。
  * nodejs - 從應用程式的所有執行個體擷取的 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。

### <a name="live-stream-tail"></a>即時資料流 (tail)
tooview 即時資料流的診斷記錄檔資訊，使用 hello hello Azure 命令列工具中的下列命令：

    azure site log tail [sitename]

這會傳回 hello 伺服器上發生更新的記錄事件資料流。 此資料流會傳回部署資訊及 stdout 和 stderr 資訊 (當 loggingEnabled 為 true 時)。

<a id="nextsteps"></a>

## <a name="next-steps"></a>後續步驟
在這個發行項您學到如何 tooenable 和存取 azure 診斷資訊。 雖然這項資訊適用於瞭解問題發生的應用程式時，它可能會指向您要使用的模組或 Node.js App Service Web 應用程式所使用的 hello 版 tooa 問題是不同於部署中使用一個 hello環境。

如需有關在 Azure 上使用模組的詳細資訊，請參閱＜ [在 Azure 應用程式中使用 Node.js 模組](../nodejs-use-node-modules-azure-apps.md)＞(英文)。

如需有關為應用程式指定 Node.js 版本的詳細資訊，請參閱＜ [在 Azure 應用程式中指定 Node.js 版本]＞(英文)。

如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode 讀我檔案]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[在 Azure 應用程式中指定 Node.js 版本]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

