---
title: "在 Linux 上的 Azure Web 應用程式中的 Node.js aaaUsing PM2 組態 |Microsoft 文件"
description: "在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態"
keywords: "azure app service, web 應用程式, nodejs, pm2, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: fb420f32-6d74-49c7-992f-0ed5616e66e7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 923783ffe656e01c43318899d1a656b553ebb5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-pm2-configuration-for-nodejs-in-azure-web-app-on-linux"></a>在 Linux 上的 Azure Web 應用程式中使用適用於 Node.js 的 PM2 組態

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


如果您設定 hello 應用程式堆疊 tooNode.js on Linux 的 Azure Web 應用程式時，會產生 hello 選項 tooset Node.js 啟動檔 hello 下列影像所示：

![設定 Node.js 啟動檔案][1]

您可以使用此選項 toodo 其中一個的 hello 下列工作：

* 指定 hello Node.js 應用程式的啟動指令碼 (例如： /bin/server.js)。
* 指定 hello PM2 組態檔案 toouse Node.js 應用程式 (例如： /foo/process.json)。
  
  > [!NOTE]
  > 如果您想要您 Node.js 處理程序 toorestart 自動修改某些檔案時，，使用 hello PM2 組態。 否則，應用程式收到變更通知時不會重新啟動 (例如，當應用程式的程式碼變更時)。
  > 
  > 

您可以檢查 hello Node.js[處理檔案文件](http://pm2.keymetrics.io/docs/usage/application-declaration/)所有 hello 選項，但以下是您可以使用為 process.json 檔案的範例：

        {
          "name"        : "worker",
          "script"      : "./bin/server.js",
          "instances"   : 1,
          "merge_logs"  : true,
          "log_date_format" : "YYYY-MM-DD HH:mm Z",
          "watch": ["./bin/server.js", "foo.txt"],
          "watch_options": {
            "followSymlinks": true,
            "usePolling"   : true,
            "interval"    : 5
          }
        }

在此組態中的重要事項 toonote 如下：

* hello"script"屬性會指定您的應用程式啟動指令碼。
* hello 」 執行個體 」 屬性會指定多少個 hello 節點程序 toolaunch 執行個體。 如果您有多個核心的較大 Vm 上執行您的應用程式，它是個不錯的主意 toomaximize 您藉由設定較高的值以下的資源。
* hello 「 監看 」 陣列指定您想 toorestart hello 節點的處理程序，其變更時的所有檔案。
* Hello"watch_options 」，您目前需要 toospecify"usePolling 」 為 true 由於 hello 已裝載您應用程式內容的方式。

## <a name="next-steps"></a>後續步驟
* [什麼是 Linux 上的 Azure Web 應用程式？](app-service-linux-intro.md)
* [Linux 上的 Azure App Service Web 應用程式常見問題集](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-nodejs-pm2/nodejs-startup-file.png
