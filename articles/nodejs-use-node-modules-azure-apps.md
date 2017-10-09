---
title: "aaaWorking Node.js 模組"
description: "深入了解如何 toowork Node.js 模組，使用 Azure 應用程式服務或雲端服務時使用。"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c0e6cd3d-932d-433e-b72d-e513e23b4eb6
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 926358b7eb80a659dbc1015686b06a30d8c9b8f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-nodejs-modules-with-azure-applications"></a>使用 Node.js 模組與 Azure 應用程式搭配
本文提供有關使用 Node.js 模組與 Azure 上代管之應用程式搭配的指引。 它提供有關確保應用程式使用模組特定版本，以及搭配原生模組與 Azure 使用的指引。

如果您已經熟悉如何使用 Node.js 模組**package.json**和**npm shrinkwrap.json**檔案 hello 下列資訊提供快速摘要的本文中所討論的內容：

* Azure App Service 熟悉 **package.json** 和 **npm-shrinkwrap.json** 檔案，並可根據這些檔案中的項目安裝模組。

* Azure 雲端服務預期 hello 開發環境中和 hello 上安裝的所有模組 toobe**節點\_模組**目錄 toobe 納入 hello 部署套件的一部分。 很可能 tooenable 支援安裝模組使用**package.json**或**npm shrinkwrap.json**檔案在雲端服務; 不過，此設定需要 hello 預設的自訂雲端服務專案所使用的指令碼。 如需如何 tooconfigure 此環境中，請參閱[Azure 啟動工作 toorun npm 安裝 tooavoid 部署節點模組](https://github.com/woloski/nodeonazure-blog/blob/master/articles/startup-task-to-run-npm-in-azure.markdown)

> [!NOTE]
> 因為在 VM 中的 hello 部署經驗是相依於 hello 虛擬機器所裝載的 hello 作業系統本文中，不會討論 azure 虛擬機器。
> 
> 

## <a name="nodejs-modules"></a>Node.js 模組
模組是指可載入的 JavaScript 封裝，可為您的應用程式提供特定功能。 模組通常會安裝使用 hello **npm**命令列工具，不過某些模組 （例如 hello http 模組） 會作為 hello 核心 Node.js 封裝的一部分。

安裝模組之後，它們儲存在 hello**節點\_模組**目錄在 hello 根目錄，您的應用程式目錄結構。 Hello 內每個模組**節點\_模組**目錄維護自己**節點\_模組**包含它相依於，而這種行為會重複任何模組的目錄每個模組 hello 相依性鏈結中向下的所有 hello 方式。 這個環境可讓每個安裝模組 toohave hello 模組自己版本需求而定，但是它可能會很大的目錄結構。

部署的 hello**節點\_模組**增加 hello 大小相較的 hello 部署的應用程式的一部分時，目錄 toousing **package.json**或**npm shrinkwrap.json**檔案; 不過，它並保證在生產環境中使用的 hello 模組 hello 版本是 hello 相同做為開發中使用的 hello 模組。

### <a name="native-modules"></a>原生模組
雖然大多數的模組是簡單的純文字 JavaScript 檔案，有些模組卻是平台特定的二進位影像。 這些模組會在安裝時編譯，通常是採用 Python 和 node-gyp。 因為 Azure 雲端服務依賴 hello**節點\_模組**資料夾被部署為 hello 應用程式，包含在雲端服務中應該工作 hello 安裝模組的一部分時，只要它是任何原生模組的一部分安裝和編譯的 Windows 開發系統上。

Azure App Service 不支援所有的原生模組，而且在編譯具有特定必要元件的模組時，可能會失敗。 雖然某些熱門模組 (如 MongoDB) 具有選擇性原生相依性，而且沒有這些相依性仍照常運作，但兩種因應措施成功證明目前幾乎可使用所有的原生模組：

* 執行**npm 安裝**已安裝的所有 hello 原生模組的必要元件的 Windows 電腦上。 接著，將部署建立 hello**節點\_模組**資料夾 hello 應用程式 tooAzure 應用程式服務的一部分。

  * 在編譯之前，檢查本機 Node.js 安裝具有相符結構，而且 hello 版本與 Azure 中使用的其中一個可能 toohello (hello 目前的值可以針對從屬性的執行階段檢查**process.arch**和**process.version**)。

* Azure App Service 可設定的 tooexecute 自訂 bash，或殼層指令碼，在部署期間，讓您 hello 機會 tooexecute 自訂命令和精確地設定 hello 方式**npm 安裝**正在執行。 為視訊的顯示方式 tooconfigure 該環境中，請參閱[自訂 Kudu 與網站部署指令碼]。

### <a name="using-a-packagejson-file"></a>使用 package.json 檔案
hello **package.json**檔案是方式 toospecify hello 最上層相依性應用程式需要，因此 hello 裝載平台可以安裝 hello 相依性，不需要您 tooinclude hello**節點\_封裝**資料夾 hello 部署的一部分。 Hello 應用程式部署完成之後，hello **npm 安裝**命令是使用的 tooparse hello **package.json**檔案，並安裝所有列出的 hello 相依性。

在開發期間，您可以使用 hello **-儲存**， **-儲存開發人員**，或**-儲存選擇性**安裝模組 tooadd hello 模組 tooyour的項目時的參數**package.json**自動檔案。 如需詳細資訊，請參閱 [npm-install](https://docs.npmjs.com/cli/install)(英文)。

一個潛在的問題，以 hello **package.json**檔案是只會指定最上層的相依性的 hello 版本。 安裝每個模組也不能指定 hello 版本而定，hello 模組，它是可能的您可能會以結束比 hello 其中一個在開發中使用不同的相依性鏈結。

> [!NOTE]
> 部署時 tooAzure 應用程式服務，如果您<b>package.json</b>檔案參考原生模組，您可能會看到錯誤類似 toohello hello 應用程式使用 Git 發行時，下列範例：
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

### <a name="using-a-npm-shrinkwrapjson-file"></a>使用 npm-shrinkwrap.json 檔案
hello **npm shrinkwrap.json**檔案是嘗試 tooaddress hello 模組版本設定的限制 hello **package.json**檔案。 Hello 時**package.json**檔案只包含最上層模組 hello，版本 hello **npm shrinkwrap.json**檔案包含 hello 完整模組相依性鏈結的 hello 版本需求。

準備好實際執行應用程式時，您可以鎖定版本需求，並建立**npm shrinkwrap.json**檔案使用 hello **npm shrinkwrap**命令。 此命令會使用目前安裝在 hello hello 版本**節點\_模組**資料夾，並將記錄這些版本 toohello **npm shrinkwrap.json**檔案。 Hello 應用程式是否已部署的 toohello 裝載環境之後，hello **npm 安裝**命令是使用的 tooparse hello **npm shrinkwrap.json**檔案，並安裝所有列出的 hello 相依性。 如需詳細資訊，請參閱 [npm-shrinkwrap](https://docs.npmjs.com/cli/shrinkwrap)。

> [!NOTE]
> 部署時 tooAzure 應用程式服務，如果您<b>npm shrinkwrap.json</b>檔案參考原生模組，您可能會看到錯誤類似 toohello hello 應用程式使用 Git 發行時，下列範例：
> 
> npm ERR! module-name@0.6.0 install: 'node-gyp configure build'
> 
> npm ERR! 'cmd "/c" "node-gyp configure build"' failed with 1
> 
> 

## <a name="next-steps"></a>後續步驟
既然您了解如何 toouse Node.js 模組，透過 Azure，深入了解如何太[指定 hello Node.js 版本]，[建置和部署 Node.js web 應用程式](app-service-web/app-service-web-get-started-nodejs.md)，和[toouse hello Azure 命令列的方式介面，用於 Mac 和 Linux]。

如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/nodejs/azure/)。

[指定 hello Node.js 版本]: nodejs-specify-node-version-azure-apps.md
[toouse hello Azure 命令列的方式介面，用於 Mac 和 Linux]:cli-install-nodejs.md
[自訂 Kudu 與網站部署指令碼]: https://channel9.msdn.com/Shows/Azure-Friday/Custom-Web-Site-Deployment-Scripts-with-Kudu-with-David-Ebbo
