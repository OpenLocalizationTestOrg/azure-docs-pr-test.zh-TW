---
title: "aaaManage hello Azure 入口網站透過 Azure Cosmos DB 帳戶 |Microsoft 文件"
description: "了解如何 toomanage Azure Cosmos DB 帳戶透過 hello Azure 入口網站。 尋找有關使用 hello Azure 入口網站 tooview、 複製、 刪除和存取帳戶的指南。"
keywords: "Azure 入口網站, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a>如何 toomanage Azure Cosmos DB 帳戶
深入了解 tooset 全域一致性，具有索引鍵，運作的方式，並刪除 Azure Cosmos DB 中的帳戶 hello Azure 入口網站。

## <a id="consistency"></a>管理 Azure Cosmos DB 一致性設定
選取 hello 右一致性層級取決於您的應用程式的 hello 語意。 您應該熟悉 Azure Cosmos DB 中的 hello 可用的一致性層級讀取[toomaximize 可用性和效能 Azure Cosmos DB 中的使用的一致性層級][consistency]。 Azure Cosmos DB 會在您資料庫帳戶可用的每個一致性層級提供一致性、可用性和效能保證。 設定您的資料庫帳戶的強式一致性層級需要您的資料是局部的 tooa 單一 Azure 區域和全域使用。 Hello 另一方面，hello 鬆散的一致性層級已繫結的失效，工作階段或最終啟用您 tooassociate 任意數目的資料庫帳戶的 Azure 區域。 hello 下列簡單步驟會告訴您如何 tooselect hello 資料庫帳戶的預設一致性層級。 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a>Azure Cosmos DB 帳戶 toospecify hello 預設一致性
1. 在 hello [Azure 入口網站](https://portal.azure.com/)，存取您的 Azure Cosmos DB 帳戶。
2. 在 hello 帳戶刀鋒視窗中，按一下 **預設一致性**。
3. 在 hello**預設一致性**刀鋒視窗中，選取 hello 新一致性層級，然後按一下 **儲存**。
    ![預設一致性工作階段][5]

## <a id="keys"></a>檢視、複製和重新產生存取金鑰
當您建立 Azure Cosmos DB 帳戶時，hello 服務就會產生兩個存取 hello Azure Cosmos DB 帳戶時可以用於驗證的主要存取金鑰。 藉由提供兩個存取金鑰，Azure Cosmos DB 可讓您使用不中斷 tooyour Azure Cosmos DB 帳戶 tooregenerate hello 索引鍵。 

在 hello [Azure 入口網站](https://portal.azure.com/)，存取 hello**金鑰**hello 資源] 功能表的 [hello] 刀鋒視窗**Azure Cosmos DB 帳戶**刀鋒視窗 tooview、 複製和重新產生 hello 存取金鑰會使用的 tooaccess Azure Cosmos DB 帳戶。

![Azure 入口網站 [金鑰] 刀鋒視窗的螢幕擷取畫面](./media/manage-account/keys.png)

> [!NOTE]
> hello**金鑰**刀鋒視窗中也包含主要和次要連接字串可能是使用的 tooconnect tooyour 帳戶從 hello[資料移轉工具](import-data.md)。
> 
> 

此刀鋒視窗上也有唯讀金鑰。 讀取和查詢為唯讀作業，建立、刪除和取代則並非唯讀作業。

### <a name="copy-an-access-key-in-hello-azure-portal"></a>Hello Azure 入口網站中複製存取金鑰
在 hello**金鑰**刀鋒視窗中，按一下 hello**複製**想 toocopy 按鈕 toohello hello 機碼的權限。

![檢視與 hello Azure 入口網站中，索引鍵 刀鋒視窗中複製存取金鑰](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a>重新產生存取金鑰
您應該變更 hello 存取金鑰 tooyour Azure Cosmos DB 帳戶 toohelp 定期更新您的連接更安全。 兩個存取金鑰指派 tooenable 您 toomaintain 連線 toohello 使用一個存取金鑰，當您重新產生 Azure Cosmos DB 帳戶 hello 其他存取金鑰。

> [!WARNING]
> 重新產生存取金鑰會影響任何相依於 hello 目前金鑰的應用程式。 使用 hello 存取金鑰 tooaccess hello Azure Cosmos DB 帳戶的所有用戶端必須更新的 toouse hello 新的金鑰。
> 
> 

如果您有應用程式或使用 hello Azure Cosmos DB 帳戶的雲端服務，您將會遺失 hello 連線如果您重新產生金鑰，除非您復原您的金鑰。 hello 下列步驟概述 hello 參與復原您金鑰的程序。

1. 更新您的應用程式程式碼 tooreference hello 次要存取金鑰的 hello Azure Cosmos DB 帳戶中的 hello 存取金鑰。
2. 重新產生 hello Azure Cosmos DB 帳戶的主要存取金鑰。 在 hello [Azure 入口網站](https://portal.azure.com/)，存取您的 Azure Cosmos DB 帳戶。
3. 在 hello **Azure Cosmos DB 帳戶**刀鋒視窗中，按一下 **金鑰**。
4. Hello 上**金鑰**刀鋒視窗中，按一下 hello 重新產生] 按鈕，然後按一下 [**確定**tooconfirm 想 toogenerate 新的金鑰。
    ![重新產生存取金鑰](./media/manage-account/regenerate-keys.png)
5. 一旦您已確認該 hello 新索引鍵是可供使用 （大約 5 分鐘之後重新產生），就會更新 hello 的應用程式程式碼 tooreference hello 新主要存取金鑰的存取金鑰。
6. 重新產生 hello 次要存取金鑰。
   
    ![重新產生存取金鑰](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> 它可能需要幾分鐘後才可以使用的 tooaccess 新產生的金鑰。 您的 Azure Cosmos DB 帳戶。
> 
> 

## <a name="get-hello--connection-string"></a>取得 hello 連接字串
tooretrieve 您的連接字串中，執行下列 hello: 

1. 在 hello [Azure 入口網站](https://portal.azure.com)，存取您的 Azure Cosmos DB 帳戶。
2. 在 hello 資源功能表上，按一下 **金鑰**。
3. 按一下 hello**複製**按鈕的下一個 toohello**主要連接字串**或**次要連接字串**方塊。 

如果您使用 hello 連接字串中的 hello [Azure Cosmos DB 資料庫移轉工具](import-data.md)，附加 hello hello 連接字串的資料庫名稱 toohello 結尾。 `AccountEndpoint=< >;AccountKey=< >;Database=< >`。

## <a id="delete"></a> 刪除 Azure Cosmos DB 帳戶
tooremove Azure Cosmos DB 帳戶從 hello Azure 入口網站，您無法再使用，以滑鼠右鍵按一下 hello 帳戶名稱，再按一下**刪除帳戶**。

![如何在帳戶 toodelete Azure Cosmos DB hello Azure 入口網站](./media/manage-account/deleteaccount.png)

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，存取您想 toodelete hello Azure Cosmos DB 帳戶。
2. 在 hello **Azure Cosmos DB 帳戶**刀鋒視窗中，以滑鼠右鍵按一下 hello 帳戶，然後按一下**刪除帳戶**。 
3. 在 hello 產生確認刀鋒視窗中，輸入您想 toodelete hello 帳戶 hello Azure Cosmos DB 帳戶名稱 tooconfirm。
4. 按一下 hello**刪除** 按鈕。

![如何在帳戶 toodelete Azure Cosmos DB hello Azure 入口網站](./media/manage-account/delete-account-confirm.png)

## <a id="next"></a>接續步驟
了解如何太[開始使用 Azure Cosmos DB 帳戶](http://go.microsoft.com/fwlink/p/?LinkId=402364)。

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
