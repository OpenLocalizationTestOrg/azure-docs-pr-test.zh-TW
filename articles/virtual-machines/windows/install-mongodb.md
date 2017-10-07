---
title: "在 Azure 中的 Windows VM 上 MongoDB aaaInstall |Microsoft 文件"
description: "了解如何在執行 Windows Server 2012 R2 的 Azure VM 上 MongoDB tooinstall 建立 hello Resource Manager 部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>在 Azure 中的 Windows VM 上安裝及設定 MongoDB
[MongoDB](http://www.mongodb.org) 是受歡迎的高效能開放原始碼 NoSQL 資料庫。 這篇文章會逐步引導您安裝和設定 Azure 中 Windows Server 2012 R2 虛擬機器 (VM) 上的 MongoDB。 您也可以[在 Azure 中的 Linux VM 上安裝 MongoDB](../linux/install-mongodb.md)。

## <a name="prerequisites"></a>必要條件
在安裝和設定 MongoDB 之前，您需要 toocreate VM，在理想情況下，加入資料磁碟 tooit。 請參閱下列文章 toocreate VM hello，並加入資料磁碟：

* 建立 Windows Server VM 使用[hello Azure 入口網站](quick-create-portal.md)或[Azure PowerShell](quick-create-powershell.md)。
* 附加資料磁碟 tooa Windows Server VM 使用[hello Azure 入口網站](attach-managed-disk-portal.md)或[Azure PowerShell](attach-disk-ps.md)。

安裝和設定 MongoDB，toobegin[登入 Windows Server VM tooyour](connect-logon.md)使用遠端桌面。

## <a name="install-mongodb"></a>安裝 MongoDB
> [!IMPORTANT]
> MongoDB 安全性功能，例如驗證和 IP 位址繫結，均非預設為已啟用。 部署 MongoDB tooa 生產環境之前，應該啟用安全性功能。 如需詳細資訊，請參閱 [MongoDB 安全性和驗證](http://www.mongodb.org/display/DOCS/Security+and+Authentication)。


1. 您已連接 tooyour 使用遠端桌面的 VM 之後，開啟 Internet Explorer 從 hello**啟動**hello VM 上的功能表。
2. Internet Explorer 第一次開啟時，選取 [使用建議的安全性、隱私權與相容性設定]，然後按一下 [確定]。
3. 預設會啟用 Internet Explorer 增強式安全性設定。 新增允許的站台 hello MongoDB 網站 toohello 清單：
   
   * 選取 hello**工具**hello 右上角的圖示。
   * 在**網際網路選項**，選取 hello**安全性**索引標籤，然後選取 hello**信任的網站**圖示。
   * 按一下 hello**網站** 按鈕。 新增*https://\*。 mongodb.org* toohello 份受信任的網站和 hello 然後關閉對話方塊。
     
     ![設定 Internet Explorer 安全性設定](./media/install-mongodb/configure-internet-explorer-security.png)
4. 瀏覽 toohello [MongoDB-下載](http://www.mongodb.org/downloads)頁面 (http://www.mongodb.org/downloads)。
5. 如有需要選取 hello **Community 伺服器**版本，然後選取 hello 最新目前穩定版本及更新版本的 Windows Server 2008 R2 64 位元。 toodownload hello 安裝程式中，按一下**下載 (msi)**。
   
    ![下載 MongoDB 安裝程式](./media/install-mongodb/download-mongodb.png)
   
    Hello 下載完成之後，請執行 hello 安裝程式。
6. 閱讀並接受 hello 授權合約。 當系統提示時，選取 [完整] 安裝。
7. Hello 最後一個畫面上，按一下**安裝**。

## <a name="configure-hello-vm-and-mongodb"></a>設定 hello VM 和 MongoDB
1. hello MongoDB 安裝程式不會更新 hello 路徑變數。 沒有 hello MongoDB `bin` path 變數中的位置，您需要 toospecify hello 完整路徑每次使用 MongoDB 的可執行檔。 tooadd hello 位置 tooyour path 變數：
   
   * 以滑鼠右鍵按一下 hello**啟動**功能表，然後選取**系統**。
   * 按一下 進階系統設定，然後按一下環境變數。
   * 在 系統變數 底下，選取 路徑，然後按一下編輯。
     
     ![設定路徑變數](./media/install-mongodb/configure-path-variables.png)
     
     新增 hello 路徑 tooyour MongoDB`bin`資料夾。 MongoDB 通常安裝在 C:\Program Files\MongoDB。 請確認 VM 上的 hello 安裝路徑。 hello 下列範例會將 hello 預設 MongoDB 安裝位置 toohello`PATH`變數：
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > 要確定 tooadd hello 開頭的分號 (`;`) 您要新增位置 tooyour tooindicate`PATH`變數。

2. 在資料磁碟上建立 MongoDB 資料和記錄檔目錄。 從 hello**啟動**功能表上，選取**命令提示字元**。 下列範例中的 hello f： 磁碟機上建立 hello 目錄
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. 以下列命令，調整 hello 路徑 tooyour 資料 hello 開頭 MongoDB 執行個體，並據以記錄目錄：
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    它可能需要幾分鐘 MongoDB tooallocate hello 日誌檔案，並開始接聽連接。 所有的記錄訊息會導向的 toohello *F:\MongoLogs\mongolog.log*檔案做為`mongod.exe`啟動伺服器，並配置日誌檔案。
   
   > [!NOTE]
   > hello 命令提示字元會保持專注在此工作上 MongoDB 執行個體正在執行時。 將保留 hello 命令提示字元視窗開啟 toocontinue 執行 MongoDB。 或者，安裝 MongoDB 作為服務，hello 下一個步驟中所述。

4. 為了更強固的 MongoDB 經驗，安裝 hello`mongod.exe`做為服務。 建立服務，即表示您不需要 tooleave 執行每的次想 toouse MongoDB 的命令提示字元。 建立 hello 服務，如下所示，據此調整 hello 路徑 tooyour 資料與記錄目錄：
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    hello 前述的命令會建立稱為 MongoDB，「 Mongo DB 」 的描述。 也會指定下列參數的 hello:
   
   * hello`--dbpath`選項會指定 hello hello 資料目錄位置。
   * hello`--logpath`選項必須是使用的 toospecify 記錄檔，因為 hello 執行中的服務並沒有命令視窗 toodisplay 輸出。
   * hello`--logappend`選項會指定 hello 服務重新啟動導致輸出 tooappend toohello 現有記錄檔。
   
   toostart hello MongoDB 服務，請執行下列命令的 hello:
   
    ```
    net start MongoDB
    ```
   
    如需建立 hello MongoDB 服務的詳細資訊，請參閱[設定 Windows 服務的 MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service)。

## <a name="test-hello-mongodb-instance"></a>測試 hello MongoDB 執行個體
當 MongoDB 執行為單一執行個體或安裝為服務，您現在可以開始建立和使用您的資料庫。 toostart hello MongoDB 系統管理命令介面開啟另一個 [命令提示字元] 視窗，從 hello**啟動**功能表上，並輸入下列命令的 hello:

```
mongo  
```

您可以列出 hello 資料庫以 hello`db`命令。 插入一些資料，如下所示︰

```
db.foo.insert( { a : 1 } )
```

搜尋資料，如下所示︰

```
db.foo.find()
```

hello 輸出是 toohello 類似下列範例程式碼：

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

結束 hello`mongo`主控台，如下所示：

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>設定防火牆和網路安全性群組規則
既然 MongoDB 已安裝且正在執行，連接埠 Windows 防火牆中開啟讓您可以從遠端連線 tooMongoDB。 toocreate 新增輸入的規則 tooallow TCP 連接埠 27017，開啟系統管理的 PowerShell 提示字元，並輸入下列命令的 hello:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

您也可以建立 hello 規則使用 hello**具有進階安全性的 Windows 防火牆**圖形化管理工具。 建立新的輸入的規則 tooallow TCP 埠 27017。

如有需要建立網路安全性群組規則 tooallow 存取 tooMongoDB 從外部 hello 現有的 Azure 虛擬網路子網路。 您可以建立 hello 網路安全性群組規則使用 hello [Azure 入口網站](nsg-quickstart-portal.md)或[Azure PowerShell](nsg-quickstart-powershell.md)。 如同 hello Windows 防火牆規則，允許 TCP 連接埠 27017 toohello 的 MongoDB VM 的虛擬網路介面。

> [!NOTE]
> TCP 連接埠 27017 是使用 MongoDB hello 預設通訊埠。 您可以變更此連接埠使用 hello`--port`參數啟動時`mongod.exe`以手動方式或從服務。 如果您變更 hello 連接埠，請確定 tooupdate hello Windows 防火牆和網路安全性群組規則 hello 先前步驟中。


## <a name="next-steps"></a>後續步驟
在本教學課程中，您學到如何 tooinstall 和設定 Windows VM 上 MongoDB。 您現在可以存取 MongoDB 上您的 Windows VM，藉由下列進階主題 hello 中的 hello [MongoDB 文件](https://docs.mongodb.com/manual/)。

