---
title: "aaaUse for Azure Cosmos DB Robomongo |Microsoft 文件"
description: "深入了解如何搭配 Azure Cosmos DB Robomongo toouse: MongoDB 帳戶的 API"
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a>使用 Robomongo 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶
tooconnect tooan Azure Cosmos DB： 使用 Robomongo MongoDB 帳戶的 API，您必須：

* 下載並安裝 [Robomongo](https://robomongo.org/)
* 具備您的 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶[連接字串](connect-mongodb-account.md)資訊

## <a name="connect-using-robomongo"></a>使用 Robomongo 來連接
tooadd Azure Cosmos DB: API for MongoDB 帳戶 toohello Robomongo MongoDB 連線，執行下列步驟的 hello。

1. 擷取您的 Azure Cosmos DB: hello 指示 MongoDB 帳戶的連接資訊的應用程式開發介面[這裡](connect-mongodb-account.md)。

    ![Hello 連接字串 刀鋒視窗的螢幕擷取畫面](./media/mongodb-robomongo/connectionstringblade.png)
2. 執行 *Robomongo.exe*

3. 按一下底下的 hello 連接按鈕**檔案**toomanage 您的連線。 然後，按一下 **建立**在 hello **MongoDB 連線**視窗，將會開啟 hello**連線設定**視窗。

4. 在 hello**連線設定**視窗中，選擇的名稱。 然後，尋找 hello**主機**和**連接埠**步驟 1 中的連接資訊在中，輸入至**位址**和**連接埠**分別.

    ![Hello Robomongo 管理連線的螢幕擷取畫面](./media/mongodb-robomongo/manageconnections.png)
5. 在 hello**驗證**索引標籤上，按一下 **執行驗證**。 然後，輸入您的 [資料庫] \(預設值是 *Admin*)、[使用者名稱] 和 [密碼]。
在步驟 1 的連接資訊中，可以找到 [使用者名稱] 和 [密碼]。

    ![Hello Robomongo 驗證 索引標籤的螢幕擷取畫面](./media/mongodb-robomongo/authentication.png)
6. 在 hello **SSL**索引標籤上，核取**使用 SSL 通訊協定**，然後變更 hello**驗證方法**太**自我簽署憑證**。

    ![Hello Robomongo SSL 索引標籤的螢幕擷取畫面](./media/mongodb-robomongo/SSL.png)
7. 最後，按一下 **測試**tooverify 您就可以 tooconnect，**儲存**。

## <a name="next-steps"></a>後續步驟
* 瀏覽 Azure Cosmos DB：適用於 MongoDB 的 API [範例](mongodb-samples.md)。
