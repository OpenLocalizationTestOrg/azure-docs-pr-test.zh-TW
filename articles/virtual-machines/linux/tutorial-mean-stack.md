---
title: "aaaCreate 平均值 Azure 中的 Linux VM 上的堆疊 |Microsoft 文件"
description: "了解 Azure 中的 Linux VM 上堆疊 toocreate MongoDB、 Express、 AngularJS 和 Node.js （平均） 的方式。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="d9656-103">在 Azure 中的 Linux VM 上建立 MongoDB、Express、AngularJS 和 Node.js (MEAN) 堆疊</span><span class="sxs-lookup"><span data-stu-id="d9656-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="d9656-104">本教學課程會示範在 Azure 中的 Linux VM 上堆疊 tooimplement MongoDB、 Express、 AngularJS 和 Node.js （平均） 的方式。</span><span class="sxs-lookup"><span data-stu-id="d9656-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="d9656-105">加入、 刪除和列出資料庫中的書籍，可讓您建立的 hello 平均堆疊。</span><span class="sxs-lookup"><span data-stu-id="d9656-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="d9656-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="d9656-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9656-107">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="d9656-107">Create a Linux VM</span></span>
> * <span data-ttu-id="d9656-108">安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="d9656-108">Install Node.js</span></span>
> * <span data-ttu-id="d9656-109">安裝 MongoDB 並設定好 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="d9656-110">安裝 Express 和設定路由 toohello 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="d9656-111">使用 AngularJS 存取 hello 路由</span><span class="sxs-lookup"><span data-stu-id="d9656-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="d9656-112">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d9656-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d9656-113">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d9656-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d9656-114">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="d9656-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d9656-115">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d9656-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="d9656-116">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="d9656-116">Create a Linux VM</span></span>

<span data-ttu-id="d9656-117">建立資源群組以 hello [az 群組建立](https://docs.microsoft.com/cli/azure/group#create)命令，並建立 Linux VM 以 hello [az vm 建立](https://docs.microsoft.com/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="d9656-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="d9656-118">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="d9656-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d9656-119">hello 下列範例會使用資源群組命名為 hello Azure CLI toocreate *myResourceGroupMEAN*在 hello *eastus*位置。</span><span class="sxs-lookup"><span data-stu-id="d9656-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="d9656-120">如果預設的金鑰位置還沒有 SSH 金鑰的話，此範例也會建立具有這些金鑰的 VM (名為 myVM)。</span><span class="sxs-lookup"><span data-stu-id="d9656-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="d9656-121">toouse 一組特定的索引鍵，使用 hello-ssh 金鑰-值 選項。</span><span class="sxs-lookup"><span data-stu-id="d9656-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

<span data-ttu-id="d9656-122">建立 hello VM 後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d9656-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
<span data-ttu-id="d9656-123">記下 hello `publicIpAddress`。</span><span class="sxs-lookup"><span data-stu-id="d9656-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="d9656-124">此位址為使用的 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="d9656-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="d9656-125">使用 hello 下列命令 toocreate 以 hello VM 的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="d9656-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="d9656-126">請確定 toouse hello 正確的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d9656-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="d9656-127">在上面的範例中，我們的 IP 位址是 13.72.77.9。</span><span class="sxs-lookup"><span data-stu-id="d9656-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="d9656-128">安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="d9656-128">Install Node.js</span></span>

<span data-ttu-id="d9656-129">[Node.js](https://nodejs.org/en/) 是建置在 Chrome V8 JavaScript 引擎上的 JavaScript 執行階段。</span><span class="sxs-lookup"><span data-stu-id="d9656-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="d9656-130">Node.js 用在此教學課程 tooset Express 會路由傳送的 hello 和 AngularJS 控制器。</span><span class="sxs-lookup"><span data-stu-id="d9656-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="d9656-131">在 hello 使用 hello bash 殼層透過 SSH，開啟 VM 上安裝 Node.js。</span><span class="sxs-lookup"><span data-stu-id="d9656-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="d9656-132">安裝 MongoDB 並設定好 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="d9656-133">[MongoDB](http://www.mongodb.com) 會將資料儲存在類似 JSON 的彈性文件中。</span><span class="sxs-lookup"><span data-stu-id="d9656-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="d9656-134">資料庫中的欄位可能會因 toodocument 文件和資料結構可以變更一段時間。</span><span class="sxs-lookup"><span data-stu-id="d9656-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="d9656-135">範例應用程式，我們會加入活頁簿記錄 tooMongoDB 包含書籍名稱、 isbn 編號、 author 和頁面數目。</span><span class="sxs-lookup"><span data-stu-id="d9656-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="d9656-136">在 hello 使用 hello bash 殼層透過 SSH，開啟 VM 上設定 hello MongoDB 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d9656-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="d9656-137">更新 hello 封裝管理員與 hello 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d9656-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="d9656-138">安裝 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="d9656-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="d9656-139">啟動 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d9656-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="d9656-140">我們還需要 tooinstall hello[主體剖析器](https://www.npmjs.com/package/body-parser-json)封裝 toohelp 我們處理 JSON 傳入要求 toohello 伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="d9656-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="d9656-141">安裝 hello npm 套件管理員。</span><span class="sxs-lookup"><span data-stu-id="d9656-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="d9656-142">安裝 hello 主體剖析器套件。</span><span class="sxs-lookup"><span data-stu-id="d9656-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="d9656-143">建立名為的資料夾*書籍*並新增名為檔案 tooit*立即轉譯 server.js*包含 hello hello web 伺服器的組態。</span><span class="sxs-lookup"><span data-stu-id="d9656-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="d9656-144">安裝 Express 和設定路由 toohello 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="d9656-145">[Express](https://expressjs.com) 是最小且具有彈性的 Node.js Web 應用程式架構，可為 Web 和行動應用程式提供功能。</span><span class="sxs-lookup"><span data-stu-id="d9656-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="d9656-146">在我們 MongoDB 資料庫從本教學課程 toopass 書籍資訊 tooand 用於 express。</span><span class="sxs-lookup"><span data-stu-id="d9656-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="d9656-147">[1](http://mongoosejs.com)提供簡單、 結構描述為基礎的解決方案 toomodel 應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="d9656-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="d9656-148">1 用於此教學課程 tooprovide hello 資料庫活頁簿結構描述。</span><span class="sxs-lookup"><span data-stu-id="d9656-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="d9656-149">安裝 Express 和 Mongoose。</span><span class="sxs-lookup"><span data-stu-id="d9656-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="d9656-150">在 hello*書籍*資料夾中，建立名為的資料夾*應用程式*並新增名為*routes.js*以 hello express 定義路由。</span><span class="sxs-lookup"><span data-stu-id="d9656-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. <span data-ttu-id="d9656-151">在 hello*應用程式*資料夾中，建立名為的資料夾*模型*並新增名為*book.js*定義 hello 書籍模型組態。</span><span class="sxs-lookup"><span data-stu-id="d9656-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="d9656-152">使用 AngularJS 存取 hello 路由</span><span class="sxs-lookup"><span data-stu-id="d9656-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="d9656-153">[AngularJS](https://angularjs.org) 提供一種 Web 架構讓您在 Web 應用程式中建立動態檢視。</span><span class="sxs-lookup"><span data-stu-id="d9656-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="d9656-154">在本教學課程中，我們可以快速使用 AngularJS tooconnect 我們的網頁，我們活頁簿的資料庫上執行的動作。</span><span class="sxs-lookup"><span data-stu-id="d9656-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="d9656-155">備份也變更 hello 目錄*書籍*(`cd ../..`)，然後建立名為的資料夾*公用*並新增名為的檔案*script.js*與 hello 控制器定義的組態。</span><span class="sxs-lookup"><span data-stu-id="d9656-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. <span data-ttu-id="d9656-156">在 hello*公用*資料夾中，建立名為*index.html* hello 網頁定義。</span><span class="sxs-lookup"><span data-stu-id="d9656-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a><span data-ttu-id="d9656-157">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d9656-157">Run hello application</span></span>

1. <span data-ttu-id="d9656-158">備份也變更 hello 目錄*書籍*(`cd ..`) 和執行這個命令來啟動伺服器 hello:</span><span class="sxs-lookup"><span data-stu-id="d9656-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="d9656-159">開啟 web 瀏覽器 toohello 位址所記錄的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="d9656-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="d9656-160">例如： http://13.72.77.9:3300 。</span><span class="sxs-lookup"><span data-stu-id="d9656-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="d9656-161">您應該會看到類似下列頁面的 hello:</span><span class="sxs-lookup"><span data-stu-id="d9656-161">You should see something like hello following page:</span></span>

    ![書籍記錄](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="d9656-163">輸入資料到 hello 的文字方塊，然後按一下**新增**。</span><span class="sxs-lookup"><span data-stu-id="d9656-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="d9656-164">例如：</span><span class="sxs-lookup"><span data-stu-id="d9656-164">For example:</span></span>

    ![新增書籍記錄](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="d9656-166">之後重新整理 hello 頁面，您會看到此頁面：</span><span class="sxs-lookup"><span data-stu-id="d9656-166">After refreshing hello page, you should see something like this page:</span></span>

    ![列出書籍記錄](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="d9656-168">您可以按一下**刪除**和移除 hello 資料庫中的 hello 開機記錄。</span><span class="sxs-lookup"><span data-stu-id="d9656-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9656-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9656-169">Next steps</span></span>

<span data-ttu-id="d9656-170">在本教學課程中，您已建立 Web 應用程式以在 Linux VM 上使用 MEAN 堆疊來留下書籍記錄。</span><span class="sxs-lookup"><span data-stu-id="d9656-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="d9656-171">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="d9656-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9656-172">建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="d9656-172">Create a Linux VM</span></span>
> * <span data-ttu-id="d9656-173">安裝 Node.js</span><span class="sxs-lookup"><span data-stu-id="d9656-173">Install Node.js</span></span>
> * <span data-ttu-id="d9656-174">安裝 MongoDB 並設定好 hello 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="d9656-175">安裝 Express 和設定路由 toohello 伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="d9656-176">使用 AngularJS 存取 hello 路由</span><span class="sxs-lookup"><span data-stu-id="d9656-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="d9656-177">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d9656-177">Run hello application</span></span>

<span data-ttu-id="d9656-178">如何前進 toohello 下一個教學課程 toolearn toosecure 網頁伺服器使用 SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="d9656-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d9656-179">使用 SSL 保護網路伺服器</span><span class="sxs-lookup"><span data-stu-id="d9656-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
