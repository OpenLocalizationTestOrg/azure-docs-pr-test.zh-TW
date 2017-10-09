---
title: "aaaAzure 函式執行階段概觀 |Microsoft 文件"
description: "Hello Azure 函式執行階段預覽的概觀"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 8ce3e5037731d499c330b395c89c90109d18d65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-runtime-overview"></a>Azure Functions 執行階段概觀

hello Azure 函式執行階段提供新方式您 tootake 利用 hello 簡化與彈性 hello Azure 函式程式設計模型內部。 根據 hello 相同開啟來源根目錄 Azure 函式、 Azure 函式執行階段會在內部部署的 tooprovide 幾乎完全相同的開發經驗 hello 雲端服務。

![Azure Functions 執行階段預覽入口網站][1]

hello Azure 函式執行階段會提供讓您 tooexperience Azure 函式的方式，再認可 toohello 雲端。 如此一來，可以移轉時，與您 toohello 雲端採取 hello 您建置的程式碼資產。  hello 執行階段也會開啟新選項，例如整夜使用內部部署電腦 toorun 批次程序的 hello 備用的運算能力。 您的組織 tooconditionally 傳送資料 tooother 系統內，這兩個內部部署和 hello 雲端中，您也可以使用裝置。

hello Azure 函式執行階段是由兩個部分所組成：
* Azure Functions 執行階段管理角色
* Azure Functions 執行階段背景工作角色

## <a name="azure-functions-management-role"></a>Azure Functions 管理角色

hello Azure 函式管理角色提供的函式內部的 hello 管理的主機。 此角色會執行下列工作的 hello:

* 裝載的 hello 函式，Azure 管理入口網站即 hello hello 同一個 hello 中看到[Azure 入口網站](https://portal.azure.com)。 這可讓您開發您的函式在 hello 相同方式與在 hello Azure 入口網站中。
* 將函式分配給多個 Functions 背景工作角色。
* 提供發佈端點，讓您直接從 Microsoft Visual Studio 發佈函式。

## <a name="azure-functions-worker-role"></a>Azure Functions 背景工作角色

hello Azure 函式背景工作角色部署 Windows 容器中，並且這是您的函式程式碼執行的位置。  您可以將多個背景工作角色部署到整個組織中，這也是讓客戶利用閒置計算能力的主要方法。

## <a name="minimum-requirements"></a>最低需求

tooget 入門 hello Azure 函式執行階段，您必須擁有一部電腦**Windows Server 2016 或 Windows 10 建立者更新**與存取 tooa **SQL Server**執行個體。

## <a name="next-steps"></a>後續步驟

安裝 hello [Azure 函式執行階段預覽](https://aka.ms/azafr)

<!--Image references-->
[1]: ./media/functions-runtime-overview/AzureFunctionsRuntime_Portal.png
