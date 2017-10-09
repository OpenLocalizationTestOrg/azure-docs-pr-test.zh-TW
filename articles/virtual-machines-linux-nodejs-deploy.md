---
title: "aaaDeploy Node.js 應用程式 tooLinux 在 Azure 虛擬機器"
description: "深入了解如何 toodeploy Node.js 應用程式 tooLinux 在 Azure 虛擬機器。"
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>部署 Node.js 應用程式 tooLinux 在 Azure 虛擬機器
本教學課程示範如何 tootake Node.js 應用程式並將它部署在 Azure 中執行的 tooLinux 虛擬機器。 在能夠執行 Node.js 任何作業系統上可依照本教學課程中的 hello 指示。

您將學習如何：

* 分叉和複製含有簡易待辦事項應用程式的 GitHub 儲存機制；
* 在建立和設定兩部 Linux 虛擬機器 Azure toorun hello 應用程式。
* 逐一查看 hello 應用程式上推送更新 toohello web 前端虛擬機器。

> [!NOTE]
> toocomplete 本教學課程中，您需要的 GitHub 帳戶與 Microsoft Azure 帳戶，並 hello 能力 toouse Git 從開發電腦。
> 
> 如果您沒有 GitHub 帳戶，您可以在 [這裡](https://github.com/join)註冊。
> 
> 如果您沒有 [Microsoft Azure](https://azure.microsoft.com/) 帳戶，您可以在[這裡](https://azure.microsoft.com/pricing/free-trial/)註冊免費試用帳戶。 這也將引導您完成註冊程序的 hello [Microsoft 帳戶](http://account.microsoft.com)如果您還沒有其中一個。 或者，如果您是 Visual Studio 訂閱者，您可以 [啟用 MSDN 權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。
> 
> 如果您的開發電腦上沒有 git，當您使用 Macintosh 或 Windows 機器時，請從 [這裡](http://www.git-scm.com)安裝 git。 如果您使用 Linux，安裝 git 使用最適合您，hello 機制，例如`sudo apt-get install git`。
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>分支和複製 hello 待辦事項應用程式
hello 本教學課程所使用的待辦事項應用程式會透過 MongoDB 執行個體，可追蹤的 TODO 清單實作簡單的 web 前端。 登入 tooGitHub 之後，請移[這裡](https://github.com/stepro/node-todo)toofind hello 應用程式和分岔會使用在 hello 右上方的 hello 連結。 這應該會在您的帳戶中建立名為 *accountname*/node-todo 的儲存機制。

現在，在您的開發電腦上複製這個儲存機制：

    git clone https://github.com/accountname/node-todo.git

我們稍後會使用此本機複本 hello 儲存機制的有點 toohello 原始程式碼進行變更時。

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>建立及設定 hello Linux 虛擬機器
Azure 充分支援使用 Linux 虛擬機器執行原始計算。 Hello 教學課程示範如何輕鬆地加速兩部 Linux 虛擬機器和部署 hello TODO 應用程式 toothem 執行的這個部分 hello web 前端上其中一個，並 hello MongoDB hello 其他執行個體。

### <a name="creating-virtual-machines"></a>建立虛擬機器
最簡單方式 toocreate hello Azure 中的新虛擬機器為 toouse hello Azure 入口網站。 按一下[這裡](https://portal.azure.com)toosign 中的並啟動 hello Azure 入口網站 web 瀏覽器中。 Hello Azure 入口網站已載入之後，完成下列步驟的 hello:

* 按一下 hello [+ 新增] 連結。
* 挑選 hello 「 計算 」 類別目錄，然後選擇 「 Ubuntu Server 14.04 LTS";
* 選取 hello 「 資源管理員 」 部署模型，然後按一下 [建立]。
* 填寫下列指導方針的 hello 基本概念：
  * 指定您稍後可以輕鬆識別的名稱；
  * 針對本教學課程，請選擇 [密碼] 驗證；
  * 使用可識別的名稱建立新的資源群組。
* Hello 虛擬機器大小，「 A1 標準 」 是合理的選擇在此教學課程。
* 如需其他設定，確保 hello 磁碟類型為 「 標準 」，並接受所有 hello 其餘的預設值。
* 開始進行的 hello 建立 hello 摘要 頁面上。

執行上述的 hello 處理兩次 toocreate 兩個 Linux 虛擬機器，一個用於 hello web 前端，另一個 hello MongoDB 執行個體。 建立 hello 虛擬機器將需要大約 5-10 分鐘。

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>指派虛擬機器的 DNS 項目
根據預設，只有透過公用 IP 位址 (例如 1.2.3.4) 才能存取 Azure 中建立的虛擬機器。 藉由指派這些 DNS 項目請 hello 機器更容易識別。

一旦 hello 入口網站會指出 hello 虛擬機器已建立，請按一下 hello hello 左導覽列中的 「 虛擬機器 」 連結，然後找出您的電腦。 針對每一部機器：

* 找出 hello Essentials 索引標籤並按一下 hello 公用 IP 位址。
* 在 hello 公用 IP 位址組態，指定 DNS 名稱標籤並儲存。

hello 入口網站可確保您指定該 hello 名稱可用。 在儲存 hello 組態之後, 您的虛擬機器會有類似的主機名稱太`machinename.region.cloudapp.azure.com`。

### <a name="connecting-toohello-virtual-machines"></a>連接 toohello 虛擬機器
您的虛擬機器已佈建時，他們會透過 SSH 是預先設定的 tooallow 遠端連線。 這是我們將使用 tooconfigure hello 虛擬機器的 hello 機制。 如果您使用 Windows 的程式開發，您必須 tooget 將 SSH 用戶端如果您還沒有其中一個。 常見的選擇是 PuTTy，您可以從 [這裡](http://www.chiark.greenend.org.uk/~sgtatham/putty/)下載。 Macintosh 與 Linux 作業系統會預先安裝一個 SSH 版本。

### <a name="configuring-hello-web-frontend-virtual-machine"></a>設定 hello Web 前端的虛擬機器
您所建立的 SSH toohello web 前端電腦使用 PuTTY，ssh 命令列或其他最愛 SSH 工具。 您應該會看到歡迎使用訊息，後面接著命令提示字元。

首先，讓我們確定 git 和節點都已安裝：

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

由於 hello 應用程式的 web 前端依賴某些原生的 Node.js 模組，我們還需要 tooinstall hello 組基本的建置工具：

    sudo apt-get install -y build-essential

最後，讓我們來安裝 Node.js 應用程式呼叫*永遠*，進而協助 toorun Node.js 伺服器應用程式：

    sudo npm install -g forever

這些是此虛擬機器 toobe 無法 toorun hello 應用程式的 web 前端上所需的所有 hello 相依性，所以請將該執行。 toodo，我們會先建立裸機先前分叉，使您可以輕鬆地發行更新 toohello 的虛擬機器 （我們稍後將說明此更新案例中），然後複製 hello 裸機複製 tooprovide hello GitHub 儲存機制的複製品 hello 的版本實際執行的儲存機制。

從開始 hello home （~） 目錄中，執行下列命令的 hello (取代*accountname*使用 GitHub 使用者帳戶名稱):

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

現在，請輸入 hello 節點 todo 目錄，並執行下列命令：

    npm install
    forever start server.js

hello 應用程式的 web 前端正在執行，但是還有一個步驟之前，您可以從網頁瀏覽器存取 hello 應用程式。 hello 您建立虛擬機器受到 Azure 資源呼叫*網路安全性群組*，這為您您佈建時 hello 虛擬機器建立。 目前，此資源只允許外部要求 tooport 22 toobe 路由 toohello 虛擬機器，可讓與 hello 機器，但沒有其他的 SSH 通訊。 因此在順序 tooview hello 待辦事項應用程式，也就是連接埠 8080 上的設定的 toorun，此連接埠也需要 toobe 開啟。

傳回 toohello Azure 入口網站，並完成下列步驟的 hello:

* 按一下左側導覽列 hello; 中的 「 資源群組 」
* 選取包含您的虛擬機器; hello 資源群組
* 在 hello 產生資源的清單，選取 hello 網路安全性群組 (hello 其中一個以保護盾圖示);
* 在 hello 屬性中，選擇 [連入的安全性規則]。
* 在 hello 工具列中，按一下 [新增]。
* 提供名稱，例如 "default-allow-todo"；
* Hello 通訊協定設定太"TCP";
* 設定 hello 目的地連接埠範圍太"8080";
* 按一下 [確定]，並等候建立 hello 安全性規則 toobe。

建立這個安全性規則之後, hello 待辦事項應用程式公開上會顯示 hello 網際網路，您可以瀏覽 tooit，執行個體使用的 URL，例如：

    http://machinename.region.cloudapp.azure.com:8080

您會發現，即使我們尚未設定 hello MongoDB 虛擬機器，hello 待辦事項應用程式會出現 toobe 相當的功能。 這是因為 hello 來源儲存機制是硬式編碼 toouse 預先部署的 MongoDB 執行個體。 一旦我們已經設定 hello MongoDB 虛擬機器，我們將會返回，並改為變更 hello 來源的程式碼 tooutilize 我們私用 MongoDB 執行個體。

### <a name="configuring-hello-mongodb-virtual-machine"></a>設定 hello MongoDB 虛擬機器
您所建立的 SSH toohello 第二部電腦使用 PuTTY，ssh 命令列或其他最愛 SSH 工具。 之後看到 hello 歡迎訊息和命令提示字元，安裝 MongoDB (這些指示取自[這裡](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

根據預設，MongoDB 會設定為只供本機存取。 此教學課程中，我們會設定 MongoDB，以便從 hello 應用程式的虛擬機器存取。 在 sudo 內容中，開啟 hello /etc/mongod.conf 檔案，並找出 hello `# network interfaces` > 一節。 變更 hello`net.bindIp`組態值太`0.0.0.0`。

> [!NOTE]
> 這項設定適用於 hello 只在本教學課程。 **不是** 建議的安全性作法，不應該用於實際執行環境。
> 
> 

現在請 hello MongoDB 服務已啟動：

    sudo service mongod restart

根據預設，MongoDB 會透過連接埠 27017 運作。 因此 hello 中相同的方式，我們需要 tooopen 連接埠 8080 上 hello web 前端的虛擬機器，我們需要 tooopen 連接埠 27017 hello MongoDB 虛擬機器上的。

傳回 toohello Azure 入口網站，並完成下列步驟的 hello:

* 按一下左側導覽列 hello; 中的 「 資源群組 」
* 選取 hello 資源群組含有 hello MongoDB 虛擬機器。
* 在 hello 產生資源的清單，選取 hello 網路安全性群組 (hello 其中一個以保護盾圖示) 以相同的名稱，您提供給 toohello MongoDB 虛擬機器; hello
* 在 hello 屬性中，選擇 [連入的安全性規則]。
* 在 hello 工具列中，按一下 [新增]。
* 提供名稱，例如 "default-allow-mongo"；
* Hello 通訊協定設定太"TCP";
* 設定 hello 目的地連接埠範圍太"27017";
* 按一下 [確定]，並等候建立 hello 安全性規則 toobe。

## <a name="iterating-on-hello-todo-application"></a>反覆運算 hello 待辦事項應用程式
目前為止，我們已佈建兩個的 Linux 虛擬機器： 其中一個執行中的 hello 應用程式的 web 前端，另一個執行 MongoDB 執行個體。 但有問題-hello web 前端不實際會尚未佈建的 hello MongoDB 執行個體使用。 我們會修正藉由更新 hello web 前端的程式碼 toouse 環境變數，而不是硬式編碼的執行個體。

### <a name="changing-hello-todo-application"></a>變更 hello 待辦事項應用程式
在您第一次複製 hello 節點 todo 儲存機制的開發電腦，開啟 hello`node-todo/config/database.js`檔案在您最愛的編輯器中，並變更 hello url hello 硬式編碼值類似`mongodb://...`太`process.env.MONGODB`。

認可您的變更，並推送 toohello GitHub master:

    git commit -am "Get MongoDB instance from env"
    git push origin master

不幸的是，這不會發行 hello 變更 toohello web 前端虛擬機器。 讓我們進行一些詳細變更 toothat 虛擬機器 tooenable 簡單但有效率的機制來發佈更新，因此您可以快速觀察 hello 變更的影響 hello hello 實際環境中。

### <a name="configuring-hello-web-frontend-virtual-machine"></a>設定 hello Web 前端的虛擬機器
還記得我們先前 hello web 前端的虛擬機器上建立裸機 hello 節點 todo 儲存機制的複製品。 事實上，此動作會建立新的 Git 遠端 toowhich 變更可推入。 不過，只要推送 toothis 遠端相當不讓開發人員使用他們的程式碼時所需的 hello 快速反覆項目模型。

什麼我們想要 toobe 無法 toodo 是確保發送 toohello 遠端儲存機制 hello 虛擬機器上的時，hello 執行待辦事項應用程式會自動更新。 幸運的是，這是含 git 的簡單 tooachieve。

Git 會公開攔截程序呼叫在特定時間 tooreact tooactions 採取 hello 儲存機制上的數的字。 這些使用指定的殼層指令碼儲存機制 hello 中`hooks`資料夾。 hello 攔截最適用 hello 自動更新案例中為 hello`post-update`事件。

SSH 工作階段 toohello web 前端虛擬機器中，變更 toohello`~/node-todo.git/hooks`目錄並加入下列內容 tooa 檔名為 hello `post-update` (取代`machinename`和`region`使用 MongoDB 虛擬機器資訊):

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

請確定這個檔案是藉由執行下列命令的 hello 可執行檔：

    chmod 755 post-update

此指令碼確保 hello 目前伺服器應用程式已停止、 hello hello 複製儲存機制中的程式碼是更新的 toohello 最新版本，符合任何更新的相依性，且 hello 伺服器重新啟動。 它也可確保該 hello 環境已設定在準備從環境變數接收我們第一個應用程式更新 tooget hello MongoDB 的執行個體。

### <a name="configuring-your-development-machine"></a>設定您的開發電腦
現在讓我們協助您在開發電腦接到 toohello web 前端的虛擬機器。 這很簡單，只新增 hello 裸機儲存機制 hello 與遠端的虛擬機器上。 執行下列命令 toodo hello (取代*使用者*與 web 前端的虛擬機器登入名稱和*machinename*和*區域*依適當情況):

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

這是所有需要的 tooenable 推入，或作用中發行時，變更 toohello web 前端的虛擬機器。

### <a name="publishing-updates"></a>發佈更新
讓我們發行 hello 發出到目前為止，使 hello 應用程式使用我們自己 MongoDB 執行個體的一項變更：

    git push azure master

您應該會看到輸出類似 toothis:

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

此命令完成之後，請嘗試重新整理網頁瀏覽器中的 hello 應用程式。 您應該能夠 toosee 這裡所呈現的 hello TODO 清單為空白，且不會再繫結的 toohello 共用部署 MongoDB 執行個體。

toocomplete hello 教學課程中，讓我們來變更另一個、 更明顯可見。 在您的開發電腦上開啟 hello node-todo/public/index.html 檔案使用您最愛的編輯器。 找出 hello jumbotron 標頭，並將變更從 「 我 Todo aholic 」 太的 我在 Azure 上 Todo aholic ！"的 hello 標題。

現在讓我們確認：

    git commit -am "Azurify hello title"

這個時間，讓我們發行 hello 變更 tooAzure 之前將它推送 tooback toohello GitHub 儲存機制：

    git push azure master

此命令完成之後，請重新整理 hello 網頁，您會看到 hello 變更。 它們能呈現最佳效果，因為發送 hello 變更後 toohello 原始遠端： 

    git push origin master

## <a name="next-steps"></a>後續步驟
本文示範過 tootake Node.js 應用程式並將它部署在 Azure 中執行的 tooLinux 虛擬機器。 toolearn 有關在 Azure 中 Linux 虛擬機器的詳細資訊請參閱[在 Azure 上的簡介 tooLinux](/documentation/articles/virtual-machines-linux-introduction/)。

如需有關如何在 Azure 上、 toodevelop Node.js 應用程式，請參閱 「 hello [Node.js 開發人員中心](/develop/nodejs/)。

