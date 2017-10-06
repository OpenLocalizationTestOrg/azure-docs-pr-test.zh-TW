---
title: "aaaLocal Git 部署 tooAzure 應用程式服務"
description: "深入了解如何本機 Git 部署 tooAzure tooenable 應用程式服務。"
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>本機 Git 部署 tooAzure 應用程式服務
本教學課程示範如何 toodeploy 您的應用程式太[Azure App Service]從本機電腦上的 Git 儲存機制。 應用程式服務支援使用這個方法以 hello**本機 Git** hello 中的部署選項[Azure 入口網站]。  
許多本文中所述的 hello Git 命令時，會執行自動建立 App Service 應用程式使用 hello [Azure 命令列介面]述[這裡](app-service-web-get-started.md)。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要：

* Git。 您可以下載 hello 安裝二進位檔案[這裡](http://www.git-scm.com/downloads)。  
* Git 基本知識。
* Microsoft Azure 帳戶。 如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details)。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的起始應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。  
> 
> 

## <a name="Step1"></a>步驟 1：建立本機儲存機制
執行下列工作 toocreate 新的 Git 儲存機制的 hello。

1. 啟動命令列工具，例如 **GitBash** (Windows) 或 **Bash** (Unix Shell)。 您可以在 OS X 系統上存取 hello 命令列透過 hello**終端機**應用程式。
2. 瀏覽應該放置 hello 內容 toodeploy toohello 目錄。
3. 使用下列命令 tooinitialize 新的 Git 儲存機制的 hello:

```bash  
git init
```

## <a name="Step2"></a>步驟 2︰認可內容
App Service 支援以各種程式設計語言建立的應用程式。 

1. 如果您的儲存機制已包含內容的略過此點，而且移動 toopoint 底下 2。 如果您的儲存機制尚未包含內容，請只要填入靜態的 .html 檔案，如下所示︰ 
   
   * 使用文字編輯器中，建立名為的新檔案**index.html**根目錄 hello hello Git 儲存機制
   * 新增 hello hello index.html hello 內容檔案，並將它儲存為下列文字： *Hello Git ！*
2. 從命令列的 hello，確認您在 hello 的 Git 儲存機制的根目錄下。 接著，使用下列命令 tooadd 檔案 tooyour 儲存機制的 hello:

```bash  
git add -A
```
3. 接下來，使用下列命令的 hello 認可 hello 變更 toohello 儲存機制：

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>步驟 3： 啟用 hello App Service 應用程式儲存機制
執行下列步驟 tooenable 您 App Service 應用程式的 Git 儲存機制的 hello。

1. 登入 toohello [Azure 入口網站]。
2. 在 App Service 應用程式的刀鋒視窗中，按一下 [設定] > [部署來源]。 依序按一下 [選擇來源]、[本機 Git 儲存機制] 以及 [確定]。  
   
    ![本機 Git 儲存機制](./media/app-service-deploy-local-git/local_git_selection.png)
3. 如果這是您第一次設定 Azure 中的儲存機制，您會需要它 toocreate 登入認證。 您將使用這些 toolog 到 hello Azure 儲存機制並將變更推播從本機 Git 儲存機制。 從應用程式的刀鋒視窗中，按一下 [設定] > [部署認證]，然後設定您的部署使用者名稱和密碼。 完成後，按一下 [儲存] 。
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>步驟 4：部署專案
使用下列步驟 toopublish hello 您應用程式 tooApp 使用本機 Git 服務。

1. 在您的應用程式] 刀鋒視窗 hello Azure 入口網站中，按一下 [**設定 > 屬性**hello **Git URL**。
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **Git URL**是 hello 遠端參照 toodeploy toofrom 本機儲存機制。 Hello 步驟中，您將使用此 URL。
2. 使用命令列的 hello，確認您是在 hello 的本機 Git 儲存機制的根目錄。
3. 使用`git remote`tooadd hello 遠端參考中所列**Git URL**步驟 1 中。 您的命令看起來類似 toohello 下列：
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > hello**遠端**命令會將具名的參考 tooa 遠端儲存機制。 在此範例中，它會為您 Web 應用程式的儲存機制建立名為 'azure' 的參考。
   > 
   > 
4. 推送您的內容 tooApp 服務使用新的 hello **azure**遠端您剛建立。

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. 返回 tooyour hello Azure 入口網站中的應用程式。 您最近發送的記錄項目應該會顯示在 hello**部署**刀鋒視窗。 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. 按一下 hello**瀏覽**已部署的 hello 應用程式 刀鋒視窗 tooverify hello 內容 hello 頂端的按鈕。 

## <a name="Step5"></a>疑難排解
hello 如下的錯誤或在 Azure 中使用 Git toopublish tooan App Service 應用程式時經常會遇到的問題：

- - -
**徵兆**： 無法 tooaccess [siteURL]: 無法 tooconnect 太 [scmAddress]

**可能的原因**： 如果 hello 應用程式不會啟動並執行，可能會發生這個錯誤。

**解析**: hello Azure 入口網站中的開始 hello 應用程式。 Git 部署將無法運作，除非 hello 應用程式正在執行。 

- - -
**徵兆**：無法解析主機 'hostname'

**可能的原因**： 會發生此錯誤如果 hello 位址資訊輸入時建立 hello 'azure' 遠端不正確。

**解析**： 使用 hello`git remote -v`命令 toolist 所有的遙控器，以及相關聯的 hello URL。 請確認 hello hello 'azure' 遠端 URL 正確。 如果需要請移除並重新建立此遠端使用 hello 正確的 URL。

- - -
**徵兆**：通常沒有參考且沒有指定；不執行任何動作。 或許您應該指定分支，例如 'master'。

**可能的原因**： 如果您不指定分支時執行 git push 作業，且 not set hello push.default 值使用 Git，可能會發生這個錯誤。

**解析**: hello 推入然後再執行作業，指定 hello 主要分支。 例如：

```bash  
git push azure master
```
- - -
**徵兆**：src refspec [branchname] 沒有任何符合項目。

**可能的原因**： 如果您嘗試在 hello 'azure' 遠端 master 以外 toopush tooa 分支，則會發生此錯誤。

**解析**: hello 推入然後再執行作業，指定 hello 主要分支。 例如：

```bash  
git push azure master
```
- - -
**徵兆**RPC 失敗；結果 = 22，HTTP 代碼 = 502。

**可能的原因**： 如果您嘗試透過 HTTPS 的 toopush 大型的 git 儲存機制，會發生此錯誤。

**解析**： 變更 hello git 設定上更大的 hello 本機 toomake hello 後置

```bash  
git config --global http.postBuffer 524288000
```
- - -
**徵兆**： 錯誤-變更認可的 tooremote 儲存機制，但不是會更新您的 web 應用程式。

**原因**：如果您打算部署包含 package.json 檔案的 Node.js 應用程式，但該檔案指出需要額外的模組，便有可能發生此錯誤。

**解決方式**︰其他包含 'npm ERR!' 的訊息 應已記錄的先前 toothis 錯誤，而且可以在 hello 失敗時提供額外的內容。 hello 下列已知導致此錯誤的原因，並且 hello 對應 'npm ERR ！' message:

* **格式錯誤的 package.json 檔案**：npm ERR! 無法讀取相依性。
* **原生模組沒有適用於 Windows 的二進位檔發佈**：
  
  * npm ERR! \`cmd "/c" "node-gyp rebuild"\` failed with 1
    
      或
  * npm ERR! [modulename@version] preinstall: \`make || gmake\`

## <a name="additional-resources"></a>其他資源
* [Git 文件](http://git-scm.com/documentation)
* [專案 Kudu 文件](https://github.com/projectkudu/kudu/wiki)
* [連續部署 tooAzure 應用程式服務](app-service-continuous-deployment.md)
* [如何 toouse PowerShell for Azure](/powershell/azure/overview)
* [如何 toouse hello Azure 命令列介面](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure 入口網站]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure 命令列介面]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
