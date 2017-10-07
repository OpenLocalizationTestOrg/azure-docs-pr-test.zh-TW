---
title: "Machine Learning web 服務的 aaaLogging |Microsoft 文件"
description: "深入了解如何 tooenable 記錄機器學習 web 服務。 記錄提供 toohelp 疑難排解 hello 應用程式開發介面的其他資訊。"
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>為 Machine Learning Web 服務啟用記錄
本文件提供記錄功能的機器學習 web 服務的 hello 資訊。 記錄提供只錯誤號碼和訊息，可以幫助您疑難排解您呼叫 toohello 機器學習 Api 之外的其他資訊。  

## <a name="how-tooenable-logging-for-a-web-service"></a>如何 tooenable 記錄 Web 服務

啟用記錄從 hello [Azure 機器學習 Web 服務](https://services.azureml.net)入口網站。 

1. 登入 toohello Azure 機器學習 Web 服務的入口網站位於[https://services.azureml.net](https://services.azureml.net)。 傳統 web 服務，您也可以取得 toohello 入口網站按一下**新的 Web 服務體驗**hello Machine Learning Studio 中的機器學習 Web 服務頁面上。

   ![新的 Web 服務體驗連結](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Hello 頂端功能表列上，按一下**Web 服務**新的 web 服務，或按一下**傳統 Web 服務**的傳統 web 服務。

   ![選取新的或傳統 Web 服務](media/machine-learning-web-services-logging/select-web-service.png)

3. 新的 web 服務，按一下 hello web 服務名稱。 傳統 web 服務中，按一下 hello web 服務名稱，然後在 hello 下一步 頁面上按一下 hello 適當的端點。

4. Hello 頂端功能表列上，按一下**設定**。

5. 設定 hello **Enable Logging**太選項*錯誤*（toolog 唯一錯誤） 或*所有*（適用於完整記錄）。

   ![選取記錄等級](media/machine-learning-web-services-logging/enable-logging.png)

6. 按一下 [儲存] 。

7. 傳統 web 服務，建立 hello **ml 診斷**容器。

   所有的 web 服務記錄檔會保留在 blob 容器，名為**ml 診斷**hello 與 hello web 服務相關聯的儲存體帳戶中。 為新的 web 服務，此容器會建立 hello 存取 hello web 服務的第一次。 傳統 web 服務，則需要 toocreate hello 容器不存在。 

   1. 在 hello [Azure 入口網站](https://portal.azure.com)，移至 toohello hello web 服務相關聯的儲存體帳戶。

   2. 在 [Blob 服務] 下，按一下 [容器]。

   3. 如果 hello 容器**ml 診斷**不存在，請按一下**+ 容器**，授與 hello 容器 hello 名稱"ml-diagnostics"，然後選取 hello**存取類型**為"Blob"。 按一下 [確定] 。

      ![選取記錄等級](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> 傳統 web 服務，hello Machine Learning Studio 中的 Web 服務儀表板也會有交換器 tooenable 記錄。 不過，記錄現在透過 hello Web Services 入口網站管理，因為您會需要 tooenable 記錄透過 hello 入口網站中這篇文章所述。 如果您已啟用登入 Studio，然後在 hello 服務入口網站，停用記錄，然後再次啟用。


## <a name="hello-effects-of-enabling-logging"></a>啟用記錄功能的 hello 效果
啟用記錄時，會將 hello 診斷和 hello web 服務端點中的錯誤記錄在 hello **ml 診斷**與 hello 使用者的工作區連結 hello Azure 儲存體帳戶中的 blob 容器。 此容器保留與這個儲存體帳戶相關聯的所有 hello 工作區的所有 hello web 服務端點的所有 hello 診斷資訊。

使用任何 hello 數個工具可用 tooexplore Azure 儲存體帳戶即可檢視 hello 記錄。 最簡單的 hello 可能是 hello Azure 入口網站中的 toonavigate toohello 儲存體帳戶中，按一下**容器**，然後按一下hello 容器**ml 診斷**。  

## <a name="log-blob-detail-information"></a>記錄檔 blob 詳細資訊
Hello 容器中的每個 blob 會保存 hello 的診斷資訊，正好有一個 hello 下列動作：

* 執行 hello 批次執行方法  
* 執行要求-回應 hello 方法  
* 要求-回應容器的初始化

hello 的每個 blob 的名稱具有下列形式的 hello 的前置詞： 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


其中_記錄類型_是 hello 下列值之一：  

* 批次  
* 分數/要求  
* 分數/初始  

