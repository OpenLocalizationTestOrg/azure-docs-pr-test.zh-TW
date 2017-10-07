---
title: "在 Azure Data Lake Store aaaEncryption |Microsoft 文件"
description: "了解 Azure Data Lake Store 中的加密和金鑰輪替方式"
services: data-lake-store
documentationcenter: 
author: yagupta
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 4/14/2017
ms.author: yagupta
ms.openlocfilehash: a9f3a2dce8232deba93005594d1e6a21e9c0cbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encryption-of-data-in-azure-data-lake-store"></a>Azure Data Lake Store 中的資料加密

Azure Data Lake Store 中的加密可協助您保護資料，實作企業安全性原則，並符合合規性需求。 本文章提供 hello 設計的概觀，並討論一些 hello 技術層面的實作。

Data Lake Store 同時支援待用資料和傳輸中資料的加密。 對於待用資料，Data Lake Store 支援「預設開啟」、透明加密。 以下是這些詞彙的更詳細說明︰

* **上預設**: hello 預設設定當您建立新的 Data Lake Store 帳戶時，啟用加密。 之後，會儲存在資料湖存放區的資料會一直持續性的媒體上的加密之前 toostoring。 這是 hello 行為的所有資料，並無法在建立帳戶之後變更。
* **透明**： 加密資料的先前 toopersisting，和解密資料的先前 tooretrieval 自動的資料湖存放區。 hello 加密 」 設定，並由系統管理員在 hello 資料湖存放區層級管理。 不會變更 toohello 資料存取 Api。 因此，因為加密而與 Data Lake Store 互動的應用程式和服務也不需要變更。

傳輸中的資料 (也稱為移動中的資料) 也一律會在 Data Lake Store 中加密。 此外 tooencrypting 資料先前 toostoring toopersistent 媒體 hello 資料也都受到保護傳輸中使用 HTTPS。 HTTPS 是 hello 唯一的通訊協定支援的資料湖存放區 REST 介面的 hello。 hello 下圖顯示資料湖存放區中加密資料會變成：

![Data Lake Store 中的資料加密圖表](./media/data-lake-store-encryption/fig1.png)


## <a name="set-up-encryption-with-data-lake-store"></a>使用 Data Lake Store 設定加密

在帳戶建立期間會設定 Data Lake Store 的加密，且預設永遠啟用。 您可以管理您自己的 hello 金鑰，或允許 Data Lake Store toomanage 加以 （這是 hello 預設值）。

如需詳細資訊，請參閱[開始使用](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal)。

## <a name="how-encryption-works-in-data-lake-store"></a>Data Lake Store 中的加密運作方式

hello 下列資訊涵蓋 toomanage 主要加密金鑰，以及它如何解釋 hello 三種不同的類型可用於資料加密的資料湖存放區索引鍵。

### <a name="master-encryption-keys"></a>主要加密金鑰

Data Lake Store 提供兩種管理主要加密金鑰 (MEK) 的模式。 現在，假設該 hello 主要加密金鑰是 hello 最上層機碼。 任何資料儲存在資料湖存放區中的必要的 toodecrypt 存取 toohello 主要加密金鑰。

如下所示為 hello 兩個模式，來管理 hello 主要加密金鑰：

*   服務管理的金鑰
*   客戶管理的金鑰

在這兩種模式中，以將其儲存在 Azure 金鑰保存庫保護 hello 主要加密金鑰。 金鑰保存庫是完全受管理高度安全服務可以使用的 toosafeguard 密碼編譯金鑰的 Azure 上。 如需詳細資訊，請參閱 [Key Vault](https://azure.microsoft.com/services/key-vault)。

以下是簡短的 hello 兩種管理 hello MEKs 模式所提供的功能比較。

|  | 服務管理的金鑰 | 客戶管理的金鑰 |
| --- | --- | --- |
|儲存資料的方式|儲存的先前 toobeing 永遠加密。|儲存的先前 toobeing 永遠加密。|
|Hello 主要加密金鑰儲存在哪裡？|金鑰保存庫|金鑰保存庫|
|是任何加密金鑰儲存在 hello 清除外部金鑰保存庫？ |否|否|
|可以 hello MEK 擷取金鑰保存庫？|否。 之後 hello MEK 會儲存在金鑰保存庫，它只能用於加密和解密。|否。 之後 hello MEK 會儲存在金鑰保存庫，它只能用於加密和解密。|
|Hello 金鑰保存庫執行個體和 hello MEK 擁有者是誰？|hello Data Lake Store 服務|您擁有 hello 金鑰保存庫執行個體，這屬於自己的 Azure 訂用帳戶。 hello MEK 金鑰保存庫中可受軟體或硬體。|
|您可以撤銷存取 toohello MEK hello Data Lake Store 服務嗎？|否|是。 您可以管理在金鑰保存庫的存取控制清單，並移除存取控制的項目 toohello 服務識別 hello Data Lake Store 服務。|
|您可以永久刪除 hello MEK 嗎？|否|是。 如果您刪除 hello MEK 從金鑰保存庫時，無法解密 hello Data Lake Store 帳戶中的 hello 資料的任何人，包括 hello Data Lake Store 服務。 <br><br> 如果您已經明確備份 hello MEK 先前 toodeleting 它從金鑰保存庫，可以還原 hello MEK，和 hello 然後可復原的資料。 不過，如果您未備份 hello MEK 先前 toodeleting 它從金鑰保存庫，hello Data Lake Store 帳戶中的 hello 資料永遠不會解密之後。|


除了這項差異的人員管理 hello MEK 和 hello 金鑰保存庫執行個體所在，hello rest hello 設計的這兩種模式是 hello 相同。

當您選擇 hello hello 模式主要加密金鑰時，很重要的 tooremember hello 下列：

*   您可以選擇 toouse 客戶管理金鑰管理服務，當您佈建 Data Lake Store 帳戶。
*   Data Lake Store 帳戶佈建之後，就無法變更 hello 模式。

### <a name="encryption-and-decryption-of-data"></a>資料的加密和解密

有三種類型的資料加密的 hello 設計中使用的索引鍵。 hello 下表提供摘要：

| Key                   | 縮寫 | 相關聯的項目 | 儲存位置                             | 類型       | 注意事項                                                                                                   |
|-----------------------|--------------|-----------------|----------------------------------------------|------------|---------------------------------------------------------------------------------------------------------|
| 主要加密金鑰 | MEK          | Data Lake Store 帳戶 | 金鑰保存庫                              | 非對稱 | 它可由 Data Lake Store 或您管理。                                                              |
| 資料加密金鑰   | DEK          | Data Lake Store 帳戶 | 永續性儲存體，由 Data Lake Store 服務管理 | 對稱  | hello MEK 加密 hello DEK。 hello 加密的 DEK 是永續性的媒體上儲存的內容。 |
| 區塊加密金鑰  | BEK          | 資料區塊 | None                                         | 對稱  | hello BEK 被衍生自 hello DEK 和 hello 資料區塊。                                                      |

hello 下列圖表將說明這些概念：

![資料加密中的加密](./media/data-lake-store-encryption/fig2.png)

#### <a name="pseudo-algorithm-when-a-file-is-toobe-decrypted"></a>虛擬演算法 toobe 解密檔案時：
1.  檢查 hello DEK hello Data Lake Store 帳戶是否為快取，並且可供使用。
    - 如果沒有，然後閱讀 hello 從永續性儲存體，加密 DEK，並將它送出 tooKey 保存庫 toobe 解密。 快取 hello 解密 DEK 在記憶體中。 已經準備好 toouse。
2.  針對每個區塊 hello 檔案中的資料：
    - 讀取永續性儲存體中的 hello 加密的資料區塊。
    - 產生從 hello DEK hello BEK 和 hello 加密的資料區塊。
    - 使用 hello BEK toodecrypt 資料。


#### <a name="pseudo-algorithm-when-a-block-of-data-is-toobe-encrypted"></a>虛擬演算法 toobe 加密的資料區塊時：
1.  檢查 hello DEK hello Data Lake Store 帳戶是否為快取，並且可供使用。
    - 如果沒有，然後閱讀 hello 從永續性儲存體，加密 DEK，並將它送出 tooKey 保存庫 toobe 解密。 快取 hello 解密 DEK 在記憶體中。 已經準備好 toouse。
2.  從 hello DEK 產生唯一 BEK hello 區塊的資料。
3.  使用 aes-256 加密來加密與 hello BEK，hello 資料區塊。
4.  永續性儲存體上的資料存放區 hello 加密的資料區塊。

> [!NOTE] 
> 基於效能考量，hello DEK hello 中的清除快取在記憶體中的一段時間，並會立即被清除之後。 持續在媒體上，它會一律加密儲存 hello MEK。

## <a name="key-rotation"></a>金鑰輪替

當您使用客戶管理的金鑰時，您可以旋轉 hello MEK。 如何查看客戶管理的金鑰，以建立 Data Lake Store 帳戶 tooset toolearn[入門](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal)。

### <a name="prerequisites"></a>必要條件

當您設定 hello Data Lake Store 帳戶時，您已選擇 toouse 您自己的金鑰。 建立 hello 帳戶之後，就無法變更此選項。 hello 下列步驟假設您使用客戶管理的金鑰 （也就是您已選擇您自己的金鑰從金鑰保存庫）。

請注意，是否您使用加密 hello 預設選項，您的資料永遠加密使用金鑰管理的資料湖存放區。 在本選項中，您不需要 hello 能力 toorotate 索引鍵，因為由資料湖存放區。

### <a name="how-toorotate-hello-mek-in-data-lake-store"></a>Toorotate hello MEK 資料湖存放區中的方式

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 瀏覽 toohello 金鑰保存庫執行個體來儲存您 Data Lake Store 帳戶相關聯的金鑰。 選取 [金鑰]。

    ![Key Vault 的螢幕擷取畫面](./media/data-lake-store-encryption/keyvault.png)

3.  選取與您的 Data Lake Store 帳戶相關聯的 hello 金鑰並建立新的版本，此機碼。 請注意，資料湖存放區目前僅支援金鑰輪替 tooa 新版本的金鑰。 它不支援繞 tooa 不同的索引鍵。

   ![[金鑰] 視窗的螢幕擷取畫面 (醒目提示 [新增版本])](./media/data-lake-store-encryption/keynewversion.png)

4.  瀏覽 toohello 資料湖存放區儲存體帳戶，並選取**加密**。

    ![Data Lake Store 儲存體帳戶視窗的螢幕擷取畫面 (醒目提示 [加密])](./media/data-lake-store-encryption/select-encryption.png)

5.  訊息會告知您金鑰新版 hello 索引鍵可供使用。 按一下**旋轉金鑰**tooupdate hello 金鑰 toohello 新版本。

    ![Data Lake Store 視窗的螢幕擷取畫面 (含有訊息並醒目提示 [輪替金鑰])](./media/data-lake-store-encryption/rotatekey.png)

這項作業花費時間不超過 2 分鐘，而且沒有預期的停機時間，因為 tookey 旋轉。 Hello 作業已完成之後，新版 hello 金鑰 hello 正在使用中。
