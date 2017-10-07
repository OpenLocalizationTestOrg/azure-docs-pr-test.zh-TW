---
title: "aaaExport hello Azure Cosmos DB 模擬器憑證 |Microsoft 文件"
description: "開發語言和執行階段，請勿使用 hello Windows 憑證存放區時將需要 tooexport，並管理 hello SSL 憑證。 這篇文章提供逐步指示。"
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB 模擬器"
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>搭配 Java、 Python 和 Node.js hello Azure Cosmos DB 模擬器憑證匯出

[**下載 hello 模擬器**](https://aka.ms/cosmosdb-emulator)

hello Azure Cosmos DB 模擬器提供本機模擬的環境，hello Azure Cosmos 資料庫服務，為開發用途，包括其使用的 SSL 連線。 這篇文章會示範如何 tooexport hello SSL 憑證以用於語言和未整合 hello Windows 憑證存放區，例如 Java 使用自己的執行階段[憑證存放區](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html)，並將其使用Python[通訊端的包裝函式](https://docs.python.org/2/library/ssl.html)和使用 Node.js [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)。 閱讀更多關於中的 hello 模擬器[使用 hello Azure Cosmos DB 模擬器進行開發和測試](./local-emulator.md)。

本教學課程涵蓋 hello 下列工作：

> [!div class="checklist"]
> * 輪替憑證
> * 匯出 SSL 憑證
> * 學習如何 toouse hello Java、 Python 和 Node.js 中的憑證

## <a name="certification-rotation"></a>憑證旋轉

憑證在 hello Azure Cosmos DB 本機模擬器產生 hello hello 模擬器執行的第一次。 有兩個憑證。 其中一個用來連線 toohello 本機模擬器，另一個用於管理 hello 模擬器中的機密資料。 您想要 tooexport hello 憑證是 hello 易記名稱 」 DocumentDBEmulatorCertificate"hello 連線憑證。

這兩個憑證，可以按一下重新產生**重設資料**從 Azure Cosmos DB 模擬器 hello Windows 系統匣中執行如下所示。 如果您重新產生 hello 憑證和其安裝到 hello Java 憑證存放區或其他位置使用它們必須 tooupdate 它們，否則您的應用程式將無法再連接 toohello 本機模擬器。

![Azure Cosmos DB 本機模擬器的重設資料](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>如何 tooexport hello Azure Cosmos DB SSL 憑證

1. 藉由執行 certlm.msc 啟動 hello Windows 憑證管理員，並瀏覽 toohello 個人-> 憑證 資料夾並開啟 hello 與 hello 易記名稱的憑證**DocumentDbEmulatorCertificate**。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 1](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. 按一下 [詳細資料]，然後按一下 [確定]。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 2](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. 按一下**複製 tooFile...**.

    ![Azure Cosmos DB 本機模擬器的匯出步驟 3](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. 按一下 [下一步] 。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 4](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. 按一下 [否，不要匯出私密金鑰 ]，然後按 [下一步]。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 5](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. 按一下 [Base-64 編碼的 X.509 (.CER)]，然後按 [下一步]。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 6](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. 指定 hello 憑證的名稱。 此案例中為 **documentdbemulatorcert**，然後按 [下一步]。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 7](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. 按一下 [完成] 。

    ![Azure Cosmos DB 本機模擬器的匯出步驟 8](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>如何 toouse hello 在 Java 中的憑證

執行 Java 應用程式或使用 hello Java 用戶端的 MongoDB 應用程式時，更容易 tooinstall hello hello Java 預設憑證存放區與憑證傳遞 hello"-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>」 旗標。 如需範例包含的 hello [Java 示範應用程式](https://localhost:8081/_explorer/index.html)hello 預設憑證存放區而定。

遵循指示進行 hello hello[加入 Java CA 憑證存放區的憑證 toohello](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 憑證至 hello 預設 Java 憑證存放區。 請記住，您會使用在 hello %java_home%目錄中執行 keytool 時。

一次 hello"CosmosDBEmulatorCertificate"SSL 憑證已安裝應用程式應能 tooconnect，而且使用 hello 本機 Azure Cosmos DB 模擬器。 如果您繼續 toohave 問題可能會想 toofollow hello[偵錯 SSL/TLS 連線](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html)發行項。 很可能 hello 憑證未安裝到 hello %JAVA_HOME%/jre/lib/security/cacerts 存放區。 針對非 hello 您更新的其中一個，例如，如果您有多個已安裝的 Java 應用程式的版本可能使用不同 cacerts 存放區。

## <a name="how-toouse-hello-certificate-in-python"></a>Toouse hello Python 中的憑證的方式

依預設 hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) hello DocumentDB API 將會無法再試一次並使用 hello SSL 憑證連接 toohello 本機模擬器時。 如果您想要 toouse SSL 驗證，不過您可以依照 hello 中的 hello 範例[Python 通訊端的包裝函式](https://docs.python.org/2/library/ssl.html)文件。

## <a name="how-toouse-hello-certificate-in-nodejs"></a>如何 toouse hello Node.js 中的憑證

依預設 hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) hello DocumentDB API 將會無法再試一次並使用 hello SSL 憑證連接 toohello 本機模擬器時。 如果您想要 toouse SSL 驗證，不過您可以依照 hello 中的 hello 範例[Node.js 文件集](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback)。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 輪替憑證
> * 匯出的 hello SSL 憑證
> * 學到如何 toouse hello Java、 Python 和 Node.js 中的憑證

您可以現在繼續 toohello 概念 > 一節，如需有關 Cosmos DB。

> [!div class="nextstepaction"]
> [全球發佈](distribute-data-globally.md) 
