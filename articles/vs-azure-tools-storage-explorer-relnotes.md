---
title: "aaaMicrosoft Azure 儲存體總管 （預覽） 版本資訊 |Microsoft 文件"
description: "Microsoft Azure 儲存體總管 (預覽) 的版本資訊"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Microsoft Azure 儲存體總管 (預覽) 版本資訊

本文章包含 hello 版本的 Azure 儲存體總管 0.8.16 的資訊 （預覽） 發行的版本，以及針對先前版本的版本資訊。

[Microsoft Azure 儲存體總管 （預覽）](./vs-azure-tools-storage-manage-with-storage-explorer.md)是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。

## <a name="version-0816-preview"></a>0.8.16 版 (預覽)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>下載 Microsoft Azure 儲存體總管 0.8.16 (預覽)
- [適用於 Windows 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)](https://go.microsoft.com/fwlink/?LinkId=708343)
- [適用於 Mac 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)](https://go.microsoft.com/fwlink/?LinkId=708342)
- [適用於 Linux 的 Microsoft Azure 儲存體總管 0.8.16 (預覽)](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>新增
* 當您開啟 blob 時，儲存體總管會提示您 tooupload hello 下載檔案在偵測到變更
* 增強的 Azure Stack 登入體驗
* 改良的 hello 效能上傳/下載許多小檔案在 hello 相同時間


### <a name="fixes"></a>修正
* 對於某些 blob 類型中，選擇太 「 取代 」 期間上傳衝突會有時產生 hello 上傳正在重新啟動。 
* 在 0.8.15 版中，上傳有時會延滯在 99%。
* 上傳時檔案 tooa 檔案共用，如果您選擇 tooupload tooa 目錄不存在，您上傳會失敗。
* 儲存體總管未正確產生共用存取簽章和資料表查詢的時間戳記。


已知問題
* 目前無法使用名稱和金鑰連接字串。 它將會修正 hello 下一個版本。 在此之前，您可以使用名稱和金鑰附加。
* 如果您嘗試 tooopen 具有無效的 Windows 檔案名稱的檔案，hello 下載將會導致找不到錯誤的檔案。
* 之後的工作上，按一下 [取消]，花費時間，該工作 toocancel。 這是 hello Azure 儲存體節點文件庫的限制。
* 完成 blob 上傳之後, 會重新整理起始 hello 上載 hello 索引標籤。 這是從先前的行為變更，而且也會導致您 toobe 回復您是在 hello 容器 toohello 根目錄。
* 如果您選擇 hello 錯誤的 PIN/智慧卡憑證，則您必須在順序 toohave toorestart 存放裝置總管忘了該決策。
* 您需要 tooreenter 認證 toofilter 訂用帳戶可能會顯示 hello 帳戶設定 面板。
* 重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。 Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。
* 雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。
* Ubuntu 14.04 上的使用者，您將需要的 tooensure GCC 已啟動 toodate-這可以透過執行 hello 來完成下列命令，然後再重新啟動您的電腦：

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Ubuntu 17.04 上的使用者，您將需要 tooinstall GConf-這可藉執行下列命令，然後再重新啟動您的電腦的 hello:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>0.8.14 版 (預覽)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>下載 Azure 儲存體總管 0.8.14 (預覽)
* [下載適用於 Windows 的 Azure 儲存體總管 0.8.14 (預覽)](https://go.microsoft.com/fwlink/?LinkId=809306)
* [下載適用於 Mac 的 Azure 儲存體總管 0.8.14 (預覽)](https://go.microsoft.com/fwlink/?LinkId=809307)
* [下載適用於 Linux 的 Azure 儲存體總管 0.8.14 (預覽)](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>新增

* 更新的電子束版本 too1.7.2 中順序 tootake 利用數個重要的安全性更新
* 您現在可以快速存取 hello 線上疑難排解指南從 hello [說明] 功能表
* 儲存體總管疑難排解[指南][2]
* [指示][ 3]連接 tooan 堆疊 Azure 訂用帳戶

### <a name="known-issues"></a>已知問題

* Hello 刪除資料夾確認對話方塊上的按鈕沒有註冊 hello Linux 上按兩下滑鼠。 因應措施是 toouse hello Enter 鍵
* 如果您選擇 hello 錯誤的 PIN/智慧卡憑證，則您必須在順序 toohave 存放裝置總管 toorestart 忘記 hello 決策
* 3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤
* hello 帳戶設定 面板中可能會顯示您需要 tooreenter 順序 toofilter 訂用帳戶中的認證
* 重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。 Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。
* 雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。 
* Ubuntu 14.04 gcc 版本更新，或升級 – 步驟 tooupgrade 安裝需求如下：

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>舊版

* [0.8.13 版](#version-0813)
* [0.8.12 / 0.8.11 / 0.8.10 版](#version-0812--0811--0810)
* [0.8.9 / 0.8.8 版](#version-089--088)
* [0.8.7 版](#version-087)
* [0.8.6 版](#version-086)
* [0.8.5 版](#version-085)
* [0.8.4 版](#version-084)
* [0.8.3 版](#version-083)
* [0.8.2 版](#version-082)
* [0.8.0 版](#version-080)
* [0.7.20160509.0 版](#version-07201605090)
* [0.7.20160325.0 版](#version-07201603250)
* [0.7.20160129.1 版](#version-07201601291)
* [0.7.20160105.0 版](#version-07201601050)
* [0.7.20151116.0 版](#version-07201511160)


### <a name="version-0813"></a>0.8.13 版
05/12/2017

#### <a name="new"></a>新增

* 儲存體總管疑難排解[指南][2]
* [指示][ 3]連接 tooan 堆疊 Azure 訂用帳戶

#### <a name="fixes"></a>修正

* 已修正︰檔案上傳先前很容易造成記憶體不足錯誤
* 已修正：您現在可以使用 PIN/智慧卡登入
* 已修正：[在入口網站中開啟] 現已可以搭配 Azure 中國、Azure 德國、Azure 美國政府及 Azure Stack 運作
* 修正問題︰ 同時上傳資料夾 tooa blob 容器，「 不合法作業 」 會有時會發生錯誤
* 已修正：先前在管理快照集時會停用 [全選]
* 已修正︰ hello hello 基底 blob 的中繼資料可能會覆寫檢視其快照集的 hello 屬性之後

#### <a name="known-issues"></a>已知問題

* 如果您選擇 hello 錯誤的 PIN/智慧卡憑證，則您必須在順序 toohave 存放裝置總管 toorestart 忘記 hello 決策
* 放大或縮小，雖然 hello 縮放層級可能會短暫地重設 toohello 預設層級
* 3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤
* hello 帳戶設定 面板中可能會顯示您需要 tooreenter 順序 toofilter 訂用帳戶中的認證
* 重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。 Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。
* 雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。 
* Ubuntu 14.04 gcc 版本更新，或升級 – 步驟 tooupgrade 安裝需求如下：

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>0.8.12 / 0.8.11 / 0.8.10 版
04/07/2017

#### <a name="new"></a>新增

* 儲存體總管即將自動關閉當您安裝更新時從 hello 更新通知
* 就地快速存取能針對您經常存取的資源提供加強的使用體驗
* 在 hello Blob 容器編輯器中，您現在可以看到租用的 blob 所屬的虛擬機器
* 您現在可以摺疊 hello 左側面板
* 探索現在就會在 hello 相同時間下載
* 在 hello Blob 容器、 檔案共用，以及資料表編輯器 toosee hello 大小的資源或選取中使用的統計資料
* 您可以現在登入 tooAzure Active Directory (AAD) 基礎堆疊 Azure 帳戶。 
* 您可以現在上載封存檔案超過 32 MB tooPremium 儲存體帳戶
* 改善協助工具支援
* 您現在可以新增受信任的 base-64 編碼 X.509 SSL 憑證將 tooEdit-&gt; SSL 憑證-&gt;匯入憑證

#### <a name="fixes"></a>修正

* 已修正︰ 在重新整理帳戶的認證之後, hello 樹狀檢視會有時不自動重新整理
* 已修正：先前針對模擬器佇列和資料表產生 SAS 會導致無效的 URL
* 已修正：進階儲存體帳戶現在可以在啟用 Proxy 時展開
* 已修正： hello 的套用按鈕 hello 帳戶如果您已選取 1 或 0 帳戶管理 頁面上將無法運作
* 已修正：上傳需要衝突解決的 Blob 可能會失敗 - 已在 0.8.11 中修正 
* 已修正：傳送意見反應的功能在 0.8.11 中無法運作 - 已在 0.8.12 中修正 

#### <a name="known-issues"></a>已知問題

* 升級之後 too0.8.10，您將需要 toorefresh 所有您的認證。
* 放大或縮小，雖然 hello 縮放層級可能會短暫地重設 toohello 預設層級。
* 3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤。
* 您需要 tooreenter 順序 toofilter 訂用帳戶中的認證可能會顯示 hello 帳戶設定 面板。
* 重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。 Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留。
* 雖然 Azure Stack 目前並不支援檔案共用，檔案共用節點仍然會出現在附加的 Azure Stack 儲存體帳戶之下。 
* Ubuntu 14.04 gcc 版本更新，或升級 – 步驟 tooupgrade 安裝需求如下：

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>0.8.9 / 0.8.8 版
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>新增

* 儲存體總管 0.8.9 將會自動下載更新的 hello 最新版本。
* Hotfix： 使用入口網站產生 SAS URI tooattach 儲存體帳戶會導致錯誤。
* 現已能針對 Blob 快照集進行建立、管理及升階。
* 您現在可以登入 tooAzure 中國、 Azure 德國和 Azure 美國政府帳戶。
* 您現在可以變更 hello 縮放層級。 使用 In、 拉遠和重設縮放 hello 檢視功能表 tooZoom hello 選項。
* Blob 和檔案的使用者中繼資料現已支援 Unicode 字元。
* 協助工具改進。
* 從 hello 更新通知，就可以檢視 hello 下一版的版本資訊。 您也可以檢視 hello 目前的版本資訊從 hello [說明] 功能表。

#### <a name="fixes"></a>修正

* 已修正︰ hello 版本號碼現在會正確顯示在 Windows [控制台] 中
* 已修正： 搜尋不再限制的 too50，000 節點
* 已修正︰ 上載 tooa 檔案共用開始永遠如果 hello 目的地目錄原本不存在
* 已修正：改善較長上傳及下載的穩定性

#### <a name="known-issues"></a>已知問題

* 放大或縮小，雖然 hello 縮放層級可能會短暫地重設 toohello 預設層級。
* 快速存取僅適用於以訂用帳戶為基礎的項目。 此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源。
* 它可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定。
* 3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤。

12/16/2016
### <a name="version-087"></a>0.8.7 版

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>新增

* 您可以選擇如何 tooresolve 衝突的更新，hello 開頭下載或複製在 hello 活動視窗的工作階段
* 將滑鼠停留在 hello 儲存體資源的索引標籤 toosee hello 完整路徑
* 當您按一下索引標籤上時，與同步處理其 hello 左側瀏覽窗格中的位置

#### <a name="fixes"></a>修正

* 已修正：儲存體總管在 Mac 上現已是受信任的應用程式
* 已修正：再次支援 Ubuntu 14.04
* 已修正︰ 有時 hello 將帳戶加入載入訂用帳戶時，UI 會閃爍
* 已修正︰ 有時並非所有的儲存體資源中所列 hello 左側瀏覽窗格
* 已修正︰ hello 動作 窗格有時顯示空白的動作
* 已修正︰ hello 從 hello 上次關閉工作階段的視窗大小是現在保留
* 已修正： 您可以開啟多個索引標籤的 hello 相同的資源使用 hello 操作功能表

#### <a name="known-issues"></a>已知問題

* 快速存取僅適用於以訂用帳戶為基礎的項目。 此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源
* 可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定
* 3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤
* 搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況
* Hello 第一次使用 hello 存放裝置總管上 macOS，您可能會看到多個提示要求使用者的權限 tooaccess keychain。 我們建議您選取永遠允許讓 hello 提示不會顯示一次

11/18/2016
### <a name="version-086"></a>0.8.6 版

#### <a name="new"></a>新增

* 您可以現在 pin 碼最常使用服務 toohello 快速存取您輕鬆瀏覽
* 現已可在多個索引標籤開啟多個編輯器。 單鍵 tooopen 暫存的索引標籤。按兩下 tooopen 永久索引標籤。您也可以按一下 hello 暫存索引標籤 toomake 它永久索引標籤
* 我們已大幅改善上傳及下載的效能和穩定性，尤其是在高效能機器上處理大型檔案的情況
* 現可在 Blob 容器內建立空白的「虛擬」資料夾
* 我們已重新推出範圍搜尋，並搭配全新增強的子字串搜尋，因此您現在將會有兩種搜尋的選項： 
    * 全域搜尋-只要 hello [搜尋] 文字方塊中輸入搜尋詞彙
    * 限定範圍的搜尋-按一下 hello 放大鏡圖示下一步 tooa 節點，然後加入搜尋詞彙 toohello hello 路徑結尾，或以滑鼠右鍵按一下並選取"Here 搜尋從"
* 已新增多種佈景主題：淺色 (預設)、深色、黑色高對比和白色高對比。 移 tooEdit-&gt;佈景主題 toochange 主題設定喜好設定
* 您可以修改 Blob 和檔案的屬性
* 我們現已支援編碼 (base64) 及未編碼的佇列訊息
* 若使用 Linux，必須為 64 位元作業系統。 針對此版本，我們僅支援 64 位元的 Ubuntu 16.04.1 LTS
* 已更新我們的標誌！

#### <a name="fixes"></a>修正

* 已修正︰畫面凍結的問題
* 已修正：增強安全性
* 已修正：有時候可能會出現重複的附加帳戶
* 已修正：具有未定義內容類型的 Blob 可能會產生例外狀況
* 已修正︰ 開啟 hello 查詢面板上的空白資料表是不可行
* 已修正：數個搜尋功能中的錯誤
* 已修正︰ 增加 hello 按下 「 多負載 」 時，從 50 too100 載入的資源數目
* 已修正：首次執行時，如果已登入某個帳戶，現在預設會選取該帳戶的所有定用帳戶 

#### <a name="known-issues"></a>已知問題

* Ubuntu 14.04 上無法執行這一版的 hello 存放裝置總管
* tooopen 多個索引標籤上，按一下相同的資源，不會持續執行的 hello 相同的資源。 另一個資源上按一下並再返回，然後按一下 hello 原始資源 tooopen 上它一次在另一個索引標籤 
* 快速存取僅適用於以訂用帳戶為基礎的項目。 此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源
* 可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定
* 3 個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤
* 搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況

10/03/2016
### <a name="version-085"></a>0.8.5 版

#### <a name="new"></a>新增

* 現在使用入口網站產生 SAS 金鑰 tooattach tooStorage 可以帳戶和資源

#### <a name="fixes"></a>修正

* 修正問題︰ 有時搜尋期間的競爭情形會造成非可展開的節點 toobecome
* 已修正︰ 「 使用 HTTP 」 不適用於 tooStorage 帳戶連線與帳戶名稱和金鑰
* 已修正：SAS 金鑰 (特別是由入口網站所產生的 SAS 金鑰) 會傳回「結尾斜線」錯誤
* 已修正：資料表匯入問題
    * 資料分割索引鍵和列索引鍵有時候會反轉
    * 「 Null 」 資料分割索引鍵無法 tooread

#### <a name="known-issues"></a>已知問題

* 搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能
* Azure 堆疊目前不支援檔案，因此嘗試 tooexpand 檔案將會顯示錯誤

09/12/2016
### <a name="version-084"></a>0.8.4 版

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>新增

* 產生的直接連結 toostorage 帳戶、 容器、 佇列、 資料表或檔案共用的共用，且容易存取 tooyour 資源-Windows 和 Mac OS 支援
* 搜尋 blob 容器、 資料表、 佇列、 檔案共用或從 hello [搜尋] 方塊的儲存體帳戶
* 您現在可以將群組 hello 資料表查詢產生器中的子句
* 從 SAS 附加帳戶及容器內對 Blob 容器、檔案共用、資料表、Blob、Blob 資料夾、檔案及目錄進行重新命名和複製/貼上
* 對 Blob 容器和檔案共用進行重新命名和複製時，現在會保留屬性和中繼資料

#### <a name="fixes"></a>修正

* 已修正：無法編輯包含布林值或二進位屬性的資料表實體

#### <a name="known-issues"></a>已知問題

* 搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能

08/03/2016
### <a name="version-083"></a>0.8.3 版

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>新增

* 對容器、資料表、檔案共用進行重新命名
* 改善查詢建立器體驗
* 能力 toosave 和載入查詢
* 直接連結 toostorage 帳戶或容器、 佇列資料表，或檔案共用，並輕鬆地存取您的資源共用 （僅限 Windows-macOS 支援即將推出 ！）
* 能力 toomanage 設定 CORS 規則

#### <a name="fixes"></a>修正

* 已修正：Microsoft 帳戶每 8 至 12 小時便需要重新驗證

#### <a name="known-issues"></a>已知問題

* 有時 hello UI 可能看似凍結-最大化 hello 視窗可協助解決此問題
* macOS 安裝可能會需要較高的權限
* 可能會顯示帳戶設定 面板中，您需要 tooreenter 順序 toofilter 訂用帳戶中的認證
* 重新命名的檔案共用、 blob 容器和資料表不會保留中繼資料或 hello 容器，例如檔案共用配額、 公用存取層級或存取原則上的其他屬性
* 重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。 Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留
* 在 SAS 附加帳戶內並無法對資源進行複製或重新命名

07/07/2016
### <a name="version-082"></a>0.8.2 版

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>新增

* 儲存體帳戶是依訂用帳戶進行群組。透過金鑰或 SAS 附加的開發儲存體和資源會顯示在 (本機和附加的) 節點之下
* 在 [Azure 帳戶設定] 面板中登出帳戶
* 設定 proxy 設定 tooenable 及管理登入
* 建立和中斷 Blob 租用
* 按一下便能開啟 Blob 容器、佇列、資料表及檔案

#### <a name="fixes"></a>修正

* 已修正：使用 .NET 或 Java 程式庫插入的佇列訊息沒有從 base64 正確解碼
* 已修正：$metrics 資料表不會針對 Blob 儲存體帳戶顯示
* 已修正：資料表節點無法用於本機 (開發) 儲存體

#### <a name="known-issues"></a>已知問題

* macOS 安裝可能會需要較高的權限

06/15/2016
### <a name="version-080"></a>0.8.0 版

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>新增

* 檔案共用支援：檢視、上傳、下載、複製檔案和目錄、SAS URI (建立和連線)
* 改善使用者體驗 SAS Uri 或帳戶金鑰以連線 tooStorage
* 匯出資料表查詢結果
* 針對資料表資料行的重新排列和自訂
* 搭配啟用的計量檢視儲存體帳戶的 $logs Blob 容器和 $metrics 資料表
* 改善匯出和匯入行為，現已包含屬性值類型

#### <a name="fixes"></a>修正

* 已修正：上傳或下載大型 Blob 可能會導致不完整的上傳/下載
* 已修正︰ 編輯、 加入或匯入實體具有數值的字串值 ("1") 會將它轉換 toodouble
* Hello 本機開發環境中已修正︰ 無法 tooexpand hello 資料表節點

#### <a name="known-issues"></a>已知問題

* $metrics 資料表不會針對 Blob 儲存體帳戶顯示
* 以程式設計方式加入的佇列訊息可能無法正確顯示如果 hello 訊息使用 Base64 編碼方式編碼

05/17/2016
### <a name="version-07201605090"></a>0.7.20160509.0 版

#### <a name="new"></a>新增

* 改善應用程式當機的錯誤處理

#### <a name="fixes"></a>修正

* 已修正在需要登入認證時，InfoBar 訊息有時候不會顯示的錯誤

#### <a name="known-issues"></a>已知問題

* 資料表： 加入、 編輯或匯入實體具有模稜兩可的數字的值，例如"1"或"1.0"，具有的屬性和 hello 使用者嘗試 toosend 為`Edm.String`，傳回透過 hello 用戶端 API 為 Edm.Double 是 hello 值

03/31/2016

### <a name="version-07201603250"></a>0.7.20160325.0 版

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>新增

* 資料表支援：針對實體的檢視、查詢、匯出、匯入及 CRUD 作業
* 佇列支援：針對訊息進行檢視、新增、清除佇列
* 針對儲存體帳戶產生 SAS URI
* TooStorage 帳戶連線使用 SAS Uri
* 更新通知。 未來的更新 tooStorage 總管
* 更新外觀與風格

#### <a name="fixes"></a>修正

* 改善效能和可靠性

### <a name="known-issues-amp-mitigations"></a>已知問題 &amp; 緩解方式

* 下載大型 Blob 檔案並無法正確運作。在我們解決此問題的期間，建議您使用 AzCopy 
* 無法再進行擷取或如果 hello 主資料夾找不到或無法寫入快取帳戶認證
* 如果我們要加入、 編輯，或匯入實體具有模稜兩可的數字的值，例如"1"或"1.0"，具有的屬性，且 hello 使用者嘗試 toosend 為`Edm.String`，傳回透過 hello 用戶端 API 為 Edm.Double 是 hello 值
* 當匯入 CSV 檔案，具有多行的記錄，hello 資料可能會取得切碎或變碼的

02/03/2016

### <a name="version-07201601291"></a>0.7.20160129.1 版

#### <a name="fixes"></a>修正

* 改善上傳、下載及複製 Blob 的整體效能

01/14/2016

### <a name="version-07201601050"></a>0.7.20160105.0 版

#### <a name="new"></a>新增

* Linux 支援 (同位功能 tooOSX)
* 新增具有共用存取簽章 (SAS) 金鑰的 Blob 容器
* 新增 Azure 中國的儲存體帳戶
* 新增具有自訂端點的儲存體帳戶
* 開啟並檢視 hello 內容的文字和圖片 blob
* 檢視及編輯 Blob 屬性和中繼資料

#### <a name="fixes"></a>修正

* 已修正： 上傳或下載大量的 blob （500 +） 有時可能會發生 hello 應用程式 toohave 白色螢幕 
* 已修正︰ 當 blob 容器的公用存取層級設定，hello 新值會更新直到您重新設定 hello 焦點 hello 容器上。 此外，hello 對話方塊太一律使用預設 「 公用存取 」，而非 hello 實際目前的值。
* 更佳的整體鍵盤/協助工具及 UI 支援
* 階層連結記錄在因大量空白字元而變得過長時便會自動換行
* SAS 對話方塊支援輸入驗證
* 本機儲存體繼續 toobe 可用，即使使用者的認證已過期
* 刪除開啟的 blob 容器時，關閉 hello 右側 hello blob 總管

#### <a name="known-issues"></a>已知問題

* Gcc 版本更新，或升級 – 步驟 tooupgrade Linux 安裝需求如下： 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>0.7.20151116.0 版

#### <a name="new"></a>新增

* macOS 及 Windows 版本
* 登入 tooview 儲存體帳戶 – 使用您組織帳戶，Microsoft 帳戶、 2FA、 等等。
* 本機開發儲存體 (使用儲存體模擬器，僅限 Windows)
* Azure Resource Manager 和傳統資源支援
* 建立及刪除 Blob、佇列或資料表
* 搜尋特定的 Blob、佇列或資料表
* 瀏覽 hello 的 blob 容器的內容
* 檢視並瀏覽目錄
* 上傳、下載及刪除 Blob 和資料夾
* 檢視及編輯 Blob 屬性和中繼資料
* 產生 SAS 金鑰
* 管理及建立儲存的存取原則 (SAP)
* 使用前置詞搜尋 Blob
* 拖曳 ' n 卸除檔案 tooupload 或下載

#### <a name="known-issues"></a>已知問題

* Blob 容器的公用存取層級設定，當 hello 新值會更新直到您重新設定 hello 容器上的 hello 焦點
* 則當您開啟 hello 對話方塊 tooset hello 公用存取層級時，永遠會顯示 「 沒有公用存取 」 hello 預設值，而非 hello 實際目前的值為
* 無法對已下載的 Blob 進行重新命名
* 活動記錄檔項目將有時"堵塞 」 在進行中狀態，當發生錯誤，並不會顯示 hello 錯誤
* 有時候當機或開啟完全白色時嘗試 tooupload 或下載大量的 blob
* 取消複製作業有時候會無法運作
* 期間建立的容器 （blob/佇列/資料表），如果輸入無效的名稱，並繼續 toocreate 在不同的容器類型的另一個您無法設定焦點的 hello 新類型
* 無法建立新資料夾或對資料夾進行重新命名




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md