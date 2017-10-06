---
title: "aaaHow toomigrate 邏輯應用程式 tooschema 版本 2015年-08-01-預覽 |Microsoft 文件"
description: "您可以輕鬆地移轉您的邏輯應用程式 toohello 最新結構描述版本。 請直接遵循下列步驟。"
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a>如何 toomigrate 邏輯應用程式 tooschema 版本 2015年-08-01-預覽
toomove 現有邏輯應用程式 toohello 新結構描述中，執行下列 hello:  

1. 在 hello Azure 入口網站中開啟邏輯應用程式  
2. 按一下 [更新結構描述]︰
   
   ![API 圖示][step1]   
   hello 更新結構描述 頁面會顯示，並提供連結 tooa 文件，提供 hello hello 新結構描述中的增強功能的詳細資料： ![API 圖示][step2]

> [!NOTE]
> 當您選取**更新結構描述**，我們會自動執行 hello 移轉步驟，並為您提供 hello 程式碼輸出。 您可以使用這個 tooupdate 您定義中，不過，請確定您遵循的良好的編碼方式，例如述 hello**最佳做法**下一節。
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a>移轉您的邏輯應用程式 toohello 最新結構描述的版本時的最佳作法：
* 複製 hello 移轉指令碼 tooa 新邏輯應用程式-不會覆寫的 hello 舊的其中一個您完成移轉的應用程式的測試和確認的 hello 如預期般運作。
* 放入生產環境 **之前** 先測試邏輯應用程式
* 移轉完成後，啟動 更新您的邏輯應用程式 toouse hello [managed Api](apis-list.md)盡可能。 例如，您可以在使用 DropBox v1 的地方開始使用 Dropbox v2。

## <a name="whats-next"></a>後續步驟
* [了解 toomanually 要如何移轉您的 Logic apps](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png






