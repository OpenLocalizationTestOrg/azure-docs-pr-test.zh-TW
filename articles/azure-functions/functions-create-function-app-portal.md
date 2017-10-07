---
title: "aaaCreate 函式中的應用程式 hello Azure 入口網站 |Microsoft 文件"
description: "Azure App Service 中建立新的函式應用程式，從 hello 入口網站。"
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/11/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: c531fc71c798edf22e25a5f4b79c15413809dc86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-from-hello-azure-portal"></a>建立函式的應用程式從 hello Azure 入口網站

Azure 的函式應用程式使用 hello Azure 應用程式服務基礎結構。 本主題說明如何 toocreate hello Azure 入口網站中的函式應用程式。 函式應用程式是裝載 hello 執行個別的函式的 hello 容器。 當您建立函式應用程式在 hello 應用程式服務的主控方案中時，函式應用程式可以使用應用程式服務的所有 hello 的功能。

## <a name="create-a-function-app"></a>建立函數應用程式

[!INCLUDE [functions-create-function-app-portal](../../includes/functions-create-function-app-portal.md)]

當您建立函數應用程式時，請提供有效的**應用程式名稱**，其中只能包含字母、數字和連字號。 不允許使用底線 (**_**) 字元。

儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。 儲存體帳戶名稱必須在 Azure 中是獨一無二的。 

建立 hello 函式應用程式之後，您可以建立個別的函式中一或多個不同的語言。 建立函式[使用 hello 網站](functions-create-first-azure-function.md#create-function)，[連續部署](functions-continuous-deployment.md)，或由[使用 FTP 上載](https://github.com/projectkudu/kudu/wiki/Accessing-files-via-ftp)。

## <a name="service-plans"></a>服務方案

Azure Functions 有兩個不同的服務方案︰取用方案和 App Service 方案。 當您的程式碼執行時，標尺外必要 toohandle 負載，然後調整-在程式碼未執行時，hello 耗用量計劃自動配置運算能力。 hello App Service 方案可讓您的函式應用程式服務的應用程式存取 tooall hello 設備。 建立您的函數應用程式時，您必須選擇您的服務方案，且目前無法變更。 如需詳細資訊，請參閱[選擇 Azure Functions 主控方案](functions-scale.md)。

如果您打算 toorun JavaScript 函式上的應用程式服務計劃，您應該選擇具有較少的核心方案。 如需詳細資訊，請參閱 hello [JavaScript 函式的參考](functions-reference-node.md#choose-single-core-app-service-plans)。

<a name="storage-account-requirements"></a>

## <a name="storage-account-requirements"></a>儲存體帳戶的需求

在建立 App Service 中的函式應用程式，您必須建立或連結 tooa 一般用途 Azure 儲存體帳戶支援 Blob、 佇列和資料表儲存體。 Azure Functions 會在內部使用「Azure 儲存體」來進行作業，例如管理觸發程序和記錄函式執行。 有些儲存體帳戶並不支援佇列和表格，例如僅限 Blob 的儲存體帳戶、Azure 進階儲存體和搭配 ZRS 複寫的一般用途儲存體帳戶。 這些帳戶會篩選掉的 hello 儲存體帳戶 刀鋒視窗建立函數應用程式時。

>[!NOTE]
>當使用 hello 耗用量主控方案，函式程式碼和繫結組態檔會儲存在 Azure 檔案儲存在 hello 主要儲存體帳戶中。 當您刪除 hello 主要儲存體帳戶時，此內容會被刪除，且無法復原。

toolearn 進一步了解儲存體帳戶類型，請參閱[簡介 hello Azure 儲存體服務](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)。 

## <a name="next-steps"></a>後續步驟

[!INCLUDE [Functions quickstart next steps](../../includes/functions-quickstart-next-steps.md)]



