---
title: "aaaDeploy Sails.js web 應用程式 tooAzure 應用程式服務 |Microsoft 文件"
description: "深入了解如何 toodeploy Node.js 應用程式的 Azure 應用程式服務。 本教學課程會示範如何 toodeploy Sails.js web 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a>部署 Sails.js web 應用程式 tooAzure 應用程式服務
本教學課程示範如何 toodeploy Sails.js 應用程式 tooAzure 應用程式服務。 您可以在 hello 過程中，搜集一些有關的一般知識 tooconfigure 您 App Service 中的 Node.js 應用程式 toorun。

在這裡，您將學習有用的技能，例如︰

* 設定在 App Service 中執行 Sails.js 應用程式。
* 部署應用程式 tooApp 服務從 hello 命令列。
* 讀取的 stderr 和 stdout 記錄 tootroubleshoot 任何部署的問題。
* 儲存原始檔控制外部的環境變數。
* 從您的應用程式存取 Azure 環境變數。
* 連接 tooa 資料庫 (MongoDB)。

您應具備 Sails.js 的使用知識。 本教學課程中不是預期的 toohelp 您問題相關 toorunning Sail.js 一般。

## <a name="cli-versions-toocomplete-hello-task"></a>CLI 版本 toocomplete hello 工作

您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：

- [Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型
- [Azure CLI 2.0](app-service-web-nodejs-sails.md) -hello 資源管理部署模型我們下一個層代 CLI

## <a name="prerequisites"></a>必要條件
* [Node.js](https://nodejs.org/)
* [Sails.js](http://sailsjs.org/get-started)
* [Git](http://www.git-scm.com/downloads)
* [Azure CLI 2.0](/cli/azure/install-az-cli2)
* Microsoft Azure 帳戶。 如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。

> [!NOTE]
> 您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。 建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a>步驟 1︰在本機建立和設定 Sails.js 應用程式
首先，請執行下列步驟 ，在部署環境中快速建立預設 Sails.js 應用程式︰

1. 您選擇的開啟 hello 命令列的終端機和`CD`tooa 工作目錄。
2. 建立 Sails.js 應用程式並加以執行︰

        sails new <app_name>
        cd <app_name>
        sails lift

    請確定您可以瀏覽 toohello http://localhost:1377 在預設首頁。

1. 接下來，啟用 Azure 記錄。 在根目錄中，建立名為的檔案`iisnode.yml`並加入下列兩行 hello:

        loggingEnabled: true
        logDirectory: iisnode

    現在已啟用記錄功能 hello [iisnode](https://github.com/tjanczuk/iisnode) Azure 應用程式服務會使用 toorun Node.js 應用程式的伺服器。 
    如需有關其運作方式的詳細資訊，請參閱[toodebug Node.js web 應用程式在 Azure App Service 中的](web-sites-nodejs-debug.md)。

2. 接著，設定 hello Sails.js 應用程式 toouse Azure 環境變數。 開啟 config/env/production.js tooconfigure 實際執行環境，並設定`port`和`hookTimeout`:

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    您可以在 [Sails.js 文件](http://sailsjs.org/documentation/reference/configuration/sails-config)中找到這些組態設定的文件。

4. 接下來，硬 hello Node.js 版本想 toouse。 Package.json，在加入 hello 下列`engines`屬性 tooset hello Node.js 版本 tooone 我們想要的。

        "engines": {
            "node": "6.9.1"
        },

5. 最後，初始化 Git 儲存機制，並認可您的檔案。 在 hello （package.json 所在） 的應用程式根目錄，請執行下列 Git 命令 hello:

        git init
        git add .
        git commit -m "<your commit message>"

您的程式碼是準備 toobe 部署。 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a>步驟 2︰建立 Azure 應用程式和部署 Sails.js

接下來，在 Azure 中建立 hello 應用程式服務資源和部署您 Sails.js 應用程式 tooit。

1. 登入 tooAzure 就像這樣：

        az login

    請依照瀏覽器與 Microsoft 帳戶具有 Azure 訂用帳戶中的 hello 提示 toocontinue hello 登入。

3. 設定應用程式服務的 hello 部署使用者。 稍後您將使用這些認證來部署程式碼。
   
        az appservice web deployment user set --user-name <username> --password <password>

3. 使用名稱建立[資源群組](../azure-resource-manager/resource-group-overview.md)。 此 Node.js 教學課程中，實際上並不需要 tooknow 它是什麼。

        az group create --location "<location>" --name my-sailsjs-app-group

    toosee 何種可能的值，您可以使用`<location>`，使用 hello `az appservice list-locations` CLI 命令。

3. 使用名稱建立「免費」[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。 在此 Node.js 教學課程中，只需知道，您可以免費使用本方案中 Web 應用程式。

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. 在 `<app_name>` 中使用唯一名稱建立新的 Web 應用程式。

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a>步驟 3︰設定和部署 Sails.js 應用程式

1. 設定新的 web 應用程式的本機 Git 部署以 hello 下列命令：

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    您會收到 JSON 輸出就像這樣，這表示該 hello 遠端 Git 儲存機制設定：

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. 將 hello URL hello JSON 中加入 Git 遠端的本機儲存機制 (稱為`azure`為了簡化)。

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. 部署您的範例程式碼 toohello `azure` Git 遠端。 出現提示時，使用您先前設定的 hello 部署認證。

        git push azure master

7. 最後，只要啟動即時 Azure 應用程式在 hello 瀏覽器中：

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    您現在應該會看到 hello 相同 Sails.js 首頁。

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a>疑難排解您的部署
如果 Sails.js 應用程式失敗原因，App Service 中，尋找 hello stderr 記錄 toohelp 進行疑難排解。
如需詳細資訊，請參閱[toodebug Node.js web 應用程式在 Azure App Service 中的](web-sites-nodejs-debug.md)。
Hello 應用程式已順利啟動，如果 hello stdout 記錄應該會顯示您 hello 熟悉訊息：

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

您可以控制在 hello hello stdout 記錄檔的資料粒度[config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging)檔案。

## <a name="connect-tooa-database-in-azure"></a>連接 tooa 在 Azure 中的資料庫
tooconnect tooa 資料庫在 Azure 中，在 Azure 中，例如 Azure SQL Database、 MySQL、 MongoDB、 Azure (Redis) 快取 」 等，建立您所選擇的 hello 資料庫，並使用 hello 對應[資料存放區的配接器](https://github.com/balderdashy/sails#compatibility)tooconnect tooit。 hello 本節中的步驟示範如何使用 tooconnect tooMongoDB [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md)資料庫，可支援 MongoDB 用戶端連線。

1. [建立具有 MongoDB 通訊協定支援的 Cosmos DB 帳戶](../documentdb/documentdb-create-mongodb-account.md)。
2. [建立 Cosmos DB 集合和資料庫](../documentdb/documentdb-create-collection.md)。 hello hello 集合名稱並不重要，但是當您從 Sails.js 連接時，需要 hello hello 資料庫名稱。
3. [尋找 hello Cosmos DB 資料庫的連接資訊](../cosmos-db/connect-mongodb-account.md#GetCustomConnection)。
2. 從命令列的終端機，安裝 hello MongoDB 配接器：

        npm install sails-mongo --save

3. 開啟 config/connections.js 並新增下列連線物件 toohello 清單 hello:

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > hello`ssl: true`選項，請務必因為[Cosmos DB 需要](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)。 
    >
    >

4. 每個環境變數 (`process.env.*`)，您需要 tooset 在應用程式服務。 toodo 終端機中的下列命令，執行的 hello。 使用您 Cosmos DB hello 連接資訊。

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    將您的設定放在 Azure 應用程式設定中，可讓敏感性資料脫離原始檔控制 (Git)。 接下來，您將設定您的開發環境 toouse hello 相同的連接資訊。
5. 開啟 config/local.js 並新增下列連線物件的 hello:

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    此設定會覆寫 config/connections.js 檔 hello 本機環境中的 hello 設定。 這個檔案會排除 hello 預設.gitignore 在專案中，因此不會儲存在 Git 中。 現在，您就可以 tooconnect tooyour Cosmos DB (MongoDB) 資料庫，從您的 Azure web 應用程式並從您的本機開發環境。
6. 開啟 config/env/production.js tooconfigure 實際執行環境，並加入下列 hello`models`物件：

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. 開啟 config/env/development.js tooconfigure 開發環境，並加入下列 hello`models`物件：

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    `migrate: 'alter'`可讓您使用資料庫移轉功能 toocreate 並輕鬆地更新集合資料庫或資料表。 不過，`migrate: 'safe'`因為 Sails.js 不允許您 toouse 用於 Azure （生產環境） 環境`migrate: 'alter'`實際執行環境中 (請參閱[Sails.js 文件](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings))。
8. 從終端機，hello[產生](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate)Sails.js[藍圖 API](http://sailsjs.org/documentation/concepts/blueprints)像平常，然後執行`sails lift`來建立具有 Sails.js 資料庫移轉 hello 資料庫。 例如：

         sails generate api mywidget
         sails lift

    hello`mywidget`此命令所產生的模型是空的但我們可以使用它 tooshow 我們有資料庫連線。
    當您執行`sails lift`，它會建立 hello 遺漏集合和 hello 的資料表模型工作流程應用程式使用。
9. 您剛建立 hello 瀏覽器中存取 hello 藍圖 API。 例如：

        http://localhost:1337/mywidget/create

    hello API 應傳回 hello 建立項目後 tooyou 在 hello 瀏覽器視窗中，這表示已順利建立您的集合。

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. 現在，推入您的變更 tooAzure，並瀏覽應用程式 tooyour toomake，仍能運作。

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. 存取 hello Azure web 應用程式的藍圖 API。 例如：

         http://<appname>.azurewebsites.net/mywidget/create

     如果 hello API 傳回另一個新的項目，Azure web 應用程式指 tooyour Cosmos DB (MongoDB) 資料庫。

## <a name="more-resources"></a>其他資源
* [在 Azure App Service 中開始使用 Node.js Web 應用程式](app-service-web-get-started-nodejs.md)
* [使用 Node.js 模組與 Azure 應用程式搭配](../nodejs-use-node-modules-azure-apps.md)
