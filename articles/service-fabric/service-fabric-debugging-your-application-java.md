---
title: "aaaDebug 在 Eclipse 中您 Azure Service Fabric 應用程式 |Microsoft 文件"
description: "開發和偵錯在 Eclipse 中的本機開發叢集上以改進 hello 可靠性和效能，您的服務。"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>使用 Eclipse 針對 Java Service Fabric 應用程式進行偵錯
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. 中的 hello 步驟來啟動本機開發叢集[設定 Service Fabric 開發環境](service-fabric-get-started-linux.md)。

2. 更新 entryPoint.sh 的 hello 服務想 toodebug，使其具有遠端偵錯參數開始 hello java 處理序。 這個檔案位於下列位置的 hello: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``。 此範例已設定連接埠 8001 來進行偵錯。

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. 更新應用程式資訊清單的 hello 藉由設定 hello 執行個體計數或 hello 複本計數 hello 服務正在偵錯 too1。 此設定可避免用來偵錯的 hello 連接埠衝突。 例如，對於無狀態服務，設定``InstanceCount="1"``和可設定狀態的服務組 hello 目標和最小複本集大小 too1，如下所示： `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``。

4. 部署 hello 應用程式。

5. 在 hello Eclipse IDE 中，選取**執行偵錯組態]-> [遠端 Java 應用程式]-> [輸入連接屬性和**並設定 hello 屬性，如下所示：

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  設定所需的時間點的中斷點，偵錯 hello 應用程式。

如果 hello 應用程式損毀，您可能也想 tooenable coredumps。 請在殼層中執行 ``ulimit -c``，如果它傳回 0，則表示未啟用核心傾印。 tooenable 無限制的 coredumps，執行下列命令的 hello: ``ulimit -c unlimited``。 您也可以確認 hello 狀態使用 hello 命令``ulimit -a``。  如果您想 tooupdate hello coredump 產生路徑時，執行``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``。 

### <a name="next-steps"></a>後續步驟

* [使用 Linux Azure 診斷來收集記錄檔](service-fabric-diagnostics-how-to-setup-lad.md)。
* [在本機監視及診斷服務](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)。
