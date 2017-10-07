---
title: "aaaMicrosoft Azure 儲存體總管 0.8.7 版 （預覽） |Microsoft 文件"
description: "Microsoft Azure 儲存體總管 0.8.7 (預覽) 的版本資訊"
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
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Microsoft Azure 儲存體總管 0.8.7 (預覽)
## <a name="overview"></a>概觀
本文章包含 hello Azure 儲存體總管 0.8.7 版預覽版本的版本資訊。

[Microsoft Azure 儲存體總管 （預覽）](./vs-azure-tools-storage-manage-with-storage-explorer.md)是獨立應用程式，可讓您 tooeasily 使用在 Windows、 macOS 和 Linux 的 Azure 儲存體資料。

## <a name="azure-storage-explorer-087-preview"></a>Azure 儲存體總管 0.8.7 (預覽)
### <a name="download-azure-storage-explorer-087-preview"></a>下載 Azure 儲存體總管 0.8.7 (預覽)
- [適用於 Windows 的 Azure 儲存體總管 0.8.7 (預覽)](https://go.microsoft.com/fwlink/?LinkId=708343)
- [適用於 Mac 的 Azure 儲存體總管 0.8.7 (預覽)](https://go.microsoft.com/fwlink/?LinkId=708342)
- [適用於 Linux 的 Azure 儲存體總管 0.8.7 (預覽)](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>新的更新
* 您可以選擇如何 tooresolve 衝突的更新，hello 開頭下載，或複製工作階段中 hello**活動**視窗。
* 將滑鼠停留在 hello 儲存體資源的索引標籤 toosee hello 完整路徑。
* 當您按一下索引標籤時，它會同步處理其 hello 左側瀏覽窗格中的位置。

### <a name="fixes"></a>修正
* 已修正：「儲存體總管」在 macOS 上現已是受信任的 App。
* 已修正：再次支援 Ubuntu 14.04。
* 已修正︰ 有時 hello 加入帳戶 UI 閃爍載入訂用帳戶時。
* 已修正︰ 有時並非所有的儲存體資源列出 hello 左方瀏覽窗格中。
* 已修正︰ hello 動作窗格有時顯示空白的動作。
* 已修正︰ hello 從 hello 上次關閉工作階段的視窗大小現在保留。
* 已修正： 您可以開啟多個索引標籤的 hello 相同的資源使用 hello 操作功能表。

### <a name="known-issues"></a>已知問題
* 「快速存取」僅適用於訂用帳戶相關項目。 此版本不支援透過金鑰或 SAS 權杖附加的本機資源或資源。
* 它可能需要快速存取幾秒 toonavigate toohello 目標資源，視您所擁有的資源數目而定。
* 三個以上的 blob 或上載 hello 在相同的檔案群組的時間可能會造成錯誤。
* 搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能或造成未處理的例外狀況。
* Hello 第一次使用 hello 存放裝置總管上 macOS，您可能會看到多個提示要求使用者的權限 tooaccess hello keychain。 我們建議您選取**永遠允許**所以不會再次顯示 hello 提示字元

## <a name="previous-releases"></a>舊版
### <a name="features"></a>特性
#### <a name="main-features"></a>主要功能
* macOS 、Linux 及 Windows 版
* 登入 tooview 依訂用帳戶的儲存體帳戶：
    * 使用您的組織帳戶、Microsoft 帳戶、2FA 等等。
    * 設定及管理 Proxy 設定
    * 登出以移除帳戶
* 連線使用 tooStorage 帳戶：
    * 帳戶名稱和金鑰
    * 自訂端點 (包含 Azure China)
    * 儲存體帳戶的 SAS URI
* Azure Resource Manager 和傳統儲存體支援
* 產生 Blob、Blob 容器、佇列、資料表或檔案共用的 SAS 金鑰
* 使用共用存取簽章 (SAS) 金鑰連接 tooblob 容器、 佇列、 資料表或檔案共用
* 管理 Blob 容器、佇列、資料表或檔案共用的「Stored Access Policies」
* 使用「儲存體模擬器」進行本機儲存體開發 (僅限 Windows)
* 建立及刪除 Blob 容器、佇列或資料表
* 檢視 $logs Blob 容器和 $metrics 資料表
* 搜尋特定的 Blob、佇列、資料表或檔案共用
* 直接連結 toostorage 帳戶或容器、 佇列、 資料表或檔案共用共用，並輕鬆地存取您的資源
* 重新命名 Blob 容器、資料表、檔案共用
* 能力 toomanage 設定 CORS 規則
* 輕鬆複製儲存體帳戶的主要和次要金鑰
* 針對上傳及下載資料的 MD5 進行檢查以確保資料完整性和一致性
* 搜尋 blob 容器、 資料表、 佇列、 檔案共用或從 hello [搜尋] 方塊的儲存體帳戶
* 您可以現在 pin 碼最常使用服務 toohello 快速存取您輕鬆瀏覽
* 現已可在多個索引標籤開啟多個編輯器。 單鍵 tooopen 暫存的索引標籤。按兩下 tooopen 永久索引標籤。您也可以按一下 hello 暫存索引標籤 toomake 它永久索引標籤
* 大幅改善上傳及下載的效能和穩定性，尤其是在高效能機器上處理大型檔案的情況
* 我們會重新導入以： hello 增強限定範圍的搜尋和新增的 hello 概念範圍時。 輸入 hello 路徑 tooa 節點透過 hello 動態顯示圖示，以滑鼠右鍵按一下->"搜尋從 Here"，或手動 tooscope 該節點。 一旦設定範圍，您可以加入 hello 路徑 toodeep 搜尋開始從該節點的搜尋詞彙 toohello end
* 已新增多種佈景主題：淺色 (預設)、深色、黑色高對比和白色高對比。
* 移 tooEdit]-> [佈景主題 toochange 主題設定喜好設定
* 若使用 Linux，必須為 64 位元作業系統
* 已更新我們的標誌！
#### <a name="blobs"></a>Blob
* 檢視 Blob 並瀏覽目錄
* 上傳、下載、刪除及複製 Blob 和資料夾
* 開啟並檢視 hello 內容的文字和圖片 blob
* 檢視及編輯 Blob 屬性和中繼資料
* 使用前置詞搜尋 Blob
* 建立及中斷 Blob 和 Blob 容器的租約
* 拖曳 ' n 卸除檔案 tooupload
* 重新命名 Blob 和資料夾
* 現可在 Blob 容器內建立空白的「虛擬」資料夾
* 您可以修改 hello Blob 和檔案屬性
#### <a name="tables"></a>資料表
* 檢視和查詢的 ODATA 實體，或使用查詢產生器 toocreate 複雜的查詢
* 新增、編輯、刪除實體
* 以 CSV 格式匯入及匯出資料表內容 (包含匯出查詢結果)
* 自訂資料行順序
* 能力 toosave 查詢
#### <a name="queues"></a>佇列
* 快速查看最近的 32 個訊息
* 新增、清除佇列、檢視訊息
* 清除佇列
* 我們將讓您 toodecide 是否要將解碼 tooencode/佇列訊息
#### <a name="file-shares"></a>檔案共用
* 檢視檔案及瀏覽目錄
* 上傳、下載、刪除及複製檔案和目錄
* 檢視檔案內容
* 重新命名檔案和目錄

### <a name="bug-fixes"></a>錯誤修正
* 已修正︰畫面凍結的問題
* 已修正：增強安全性

### <a name="known-issues"></a>已知問題
* 搜尋功能在處理超過大約 50,000 個節點的搜尋作業之後，可能會影響效能，macOS 安裝可能需要提高權限
* 帳戶設定 面板中可能會顯示您需要 tooreenter 認證 toofilter 訂用帳戶
* 重新命名 Blob (個別執行或在重新命名的 Blob 容器內) 不會保留快照集。 Blob、檔案和實體的所有其他屬性和中繼資料都會在重新命名期間保留
* Azure 堆疊目前不支援檔案，因此嘗試 tooexpand hello**檔案**節點會導致錯誤
* 在 Linux 14.04 安裝需要更新或升級 gcc 版本。 hello 下列步驟說明如何 tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>舊版
#### <a name="october-2016-release-version-085"></a>2016 年 10 月版本 (0.8.5 版)
* [下載 Windows 版](https://go.microsoft.com/fwlink/?LinkId=809306)
* [下載 Mac 版](https://go.microsoft.com/fwlink/?LinkId=809307)
* [下載 Linux 版](https://go.microsoft.com/fwlink/?LinkId=809308)
