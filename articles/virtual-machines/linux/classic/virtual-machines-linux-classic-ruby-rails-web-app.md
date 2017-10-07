---
title: "aaaHost 滑軌 Linux VM 上的網站上的 Ruby |Microsoft 文件"
description: "在使用 Linux 虛擬機器的 Azure 上設定及裝載 Ruby on Rails 型網站。"
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Azure VM 上的 Ruby on Rails Web 應用程式
本教學課程示範如何 toohost Ruby 滑軌網站上使用 Linux 虛擬機器的 Azure 上。  

此教學課程使用 Ubuntu Server 14.04 LTS 通過驗證。 如果您使用不同的 Linux 散發套件，您可能需要 toomodify hello 步驟 tooinstall 滑軌。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。  本文說明如何使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。
>
>

## <a name="create-an-azure-vm"></a>建立 Azure VM
開始使用 Linux 映像建立 Azure VM。

toocreate hello VM，您可以使用 hello Azure 入口網站或 hello Azure 命令列介面 (CLI)。

### <a name="azure-portal"></a>Azure 入口網站
1. 登入 hello [Azure 入口網站](https://portal.azure.com)
2. 按一下**新增**，然後輸入 hello [搜尋] 方塊中的 < Ubuntu Server 14.04 >。 按一下 hello hello 搜尋所傳回的項目。 Hello 部署模型中，選取**傳統**，然後按一下 [建立]。
3. 在 hello 基本概念刀鋒視窗中，提供所需的 hello 欄位的值: （適用於 hello VM) 的名稱、 使用者名稱、 驗證類型以及 hello 對應的認證、 Azure 訂用帳戶、 資源群組和位置。

   ![Create a new Ubuntu Image](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Hello VM 已佈建之後，按一下 hello VM 名稱，然後按一下**端點**在 hello**設定**類別目錄。 找不到 hello SSH 端點，底下所列**獨立**。

   ![預設端點](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Azure CLI
中的 hello 步驟[建立執行 Linux 之虛擬機器][vm-instructions]。

Hello VM 已佈建之後，您可以藉由執行下列命令的 hello 取得 hello SSH 的端點：

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>安裝 Ruby on Rails
1. 使用 SSH tooconnect toohello VM。
2. 從 hello SSH 工作階段，使用下列命令 tooinstall Ruby hello VM 上的 hello:

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    hello 安裝可能需要幾分鐘的時間。 完成之後，使用下列命令 tooverify Ruby 已安裝的 hello:

        ruby -v

3. 使用 hello 下列命令 tooinstall 滑軌：

        sudo gem install rails --no-rdoc --no-ri -V

    使用 hello-否 rdoc 和--無 ri 旗標 tooskip 安裝 hello 文件集，這種方式快。
    此命令很可能會很長的時間 tooexecute，因此加入 hello-V 會顯示 hello 安裝進度的相關資訊。

## <a name="create-and-run-an-app"></a>建立及執行應用程式
仍透過 SSH 登入，執行下列命令的 hello:

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

hello[新](http://guides.rubyonrails.org/command_line.html#rails-new)命令會建立新的滑軌應用程式。 hello[伺服器](http://guides.rubyonrails.org/command_line.html#rails-server)啟動 hello WEBrick 滑軌所隨附的 web 伺服器的命令。 （用於實際執行環境，您可能會想 toouse 不同的伺服器，例如獨角獸或旅客。）

您應該會看到類似 toohello 下列輸出。

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>新增端點。
1. 前往 [Azure 入口網站] toohello [https://portal.azure.com] 並選取您的 VM。

2. 選取**端點**在 hello**設定**沿著 hello 左邊的緣 hello 頁面。

3. 按一下**新增**hello 頁面頂端的 hello。

4. 在 hello**加入端點**對話方塊頁面上，輸入下列資訊的 hello:

   * **名稱**：HTTP
   * **通訊協定**：TCP
   * **公用連接埠**：80
   * **私用連接埠**：3000
   * **浮動 IP 位址**：已停用
   * **存取控制清單順序**: 1001，或另一個值，此存取規則 hello 優先權設定。
   * **存取控制清單 - 名稱**：allowHTTP
   * **存取控制清單 - 動作**：允許
   * **存取控制清單 - 遠端子網路**：1.0.0.0/16

     此端點都有會路由傳送流量 toohello 私用連接埠 3000、 hello 滑軌伺服器正在接聽所在的 80 的公用連接埠。 hello 存取控制清單規則可讓公用連接埠 80 上的流量。

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. 按一下 [確定] toosave hello 端點。

6. 此時應會出現一則訊息，指出「正在儲存虛擬機器端點」。 此訊息會消失，一旦 hello 端點為作用中。 現在，您可能會測試您的應用程式瀏覽您的虛擬機器 toohello DNS 名稱。 hello 網站應該會出現類似 toohello 下列：

    ![預設 rails 頁面][default-rails-cloud]

## <a name="next-steps"></a>後續步驟
在本教學課程中，您所執行大部分的 hello 步驟手動。 在實際執行環境中，您會在開發電腦上撰寫應用程式，並將其部署 toohello Azure VM。 此外，大部分的實際執行環境裝載 hello 滑軌應用程式搭配另一個伺服器處理序，例如 Apache 或 NginX，以處理要求的 hello 滑軌應用程式和服務靜態資源的路由 toomultiple 執行個體。 如需詳細資訊，請參閱 http://rubyonrails.org/deploy/。

toolearn 深入了解 Ruby 上滑軌中，瀏覽 hello[拼音滑軌輔助線][rails-guides]。

toouse 從 Ruby 應用程式的 Azure 服務，請參閱：

* [使用 Blob 儲存非結構化資料][blobs]
* [使用資料表儲存機碼/值組][tables]
* [提供高頻寬內容以 hello 內容傳遞網路][cdn-howto]

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
