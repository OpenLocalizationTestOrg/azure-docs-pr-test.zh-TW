---
title: "aaaManaging Redis 快取使用 hello 適用於 Eclipse 的 Azure Explorer |Microsoft 文件"
description: "了解如何 toomanage 您的 Azure redis 快取使用 hello Azure 總管 for Eclipse。"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a>管理使用 hello Azure 總管適用於 Eclipse 的 Redis 快取

hello Azure 總管 中，這是 hello Azure Toolkit for Eclipse 的一部分，提供方便使用解決方案的 Java 開發人員管理 redis 快取內從其 Azure 帳戶中的 hello Eclipse IDE。

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a>使用 Eclipse 建立 Redis 快取

hello 步驟引導您完成 hello 步驟 toocreate 使用 hello Azure 總管的 redis 快取。

1. 使用中 hello hello 步驟的 Azure 帳戶登入 tooyour[符號中的 hello Azure Toolkit for Eclipse 指示]發行項。

1. 在 hello **Azure 總管**工具視窗中，展開 hello **Azure**  節點，以滑鼠右鍵按一下**Redis 快取**，然後按一下**建立 Redis 快取**。

   ![建立 Redis 快取功能表][CR01]

1. 當 hello**新增 Redis 快取**出現對話方塊，請指定下列選項的 hello:

   ![建立新的 Redis 快取對話方塊][CR02]

   a. **DNS 名稱**： 指定 hello 新 redis 快取，則預先決定太 hello DNS 子網域 」。 redis.cache.windows.net"; 例如： *wingtiptoys.redis.cache.windows.net*。

   b. **訂用帳戶**： 指定 hello 想 toouse hello 新 redis 快取的 Azure 訂用帳戶。

   c. **資源群組**： 指定 hello redis 快取的資源群組，您需要的下列選項的 hello toochoose 其中一個：
      * **建立新**： 指定您想 toocreate 新的資源群組。
      * **使用現有**︰指定您將從與您 Azure 帳戶相關聯的資源群組清單中進行選擇。

   d. **位置**： 指定 hello 位置建立 redis 快取的位置; 例如，*美國西部*。

   e. **定價層**： 指定您的 redis 快取會使用哪一個定價層，此設定會決定用戶端連線的 hello 數目。 (如需詳細資訊，請參閱 [Redis 快取定價]。)

   f. **非 SSL 連接埠**：指定 Redis 快取是否可允許非 SSL 連線；預設只允許 SSL 連線。

1. 指定所有的 Redis 快取設定後，請按一下 [確定]。

建立 redis 快取之後，它就會顯示在 hello Azure 總管。

   ![Azure Explorer 中的 Redis 快取][CR03]

> [!NOTE]
>
> 如需有關設定您的 Azure redis 快取設定，請參閱[如何 tooconfigure Azure Redis 快取]。
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a>Redis 快取在 Eclipse 中顯示 hello 屬性

1. 在 hello Azure 總管，以滑鼠右鍵按一下您的 redis 快取，按一下 **顯示屬性**。

   ![Azure 總管內容功能表 toodisplay 屬性 redis 快取][SP01]

1. hello Azure 總管會顯示 hello redis 快取的屬性。

   ![Redis 快取屬性][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a>使用 Eclipse 刪除 Redis 快取

1. 在 hello Azure 總管，以滑鼠右鍵按一下您的 redis 快取，按一下 **刪除**。

   ![Azure 總管內容功能表 toodelete redis 快取][DE01]

1. 按一下**確定**時提示 toodelete redis 快取。

   ![刪除 Redis 快取提示][DE02]

## <a name="next-steps"></a>後續步驟

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

如需 Azure redis 快取、 組態設定和定價的詳細資訊，請參閱下列連結查看 hello:

* [Azure Redis 快取]
* [Redis 快取文件]
* [Redis 快取定價]
* [如何 tooconfigure Azure Redis 快取]

<!-- URL List -->

[Redis 快取定價]: https://azure.microsoft.com/pricing/details/cache/
[Azure Redis 快取]: https://azure.microsoft.com/services/cache/
[Redis 快取文件]: ./redis-cache/index.md
[如何 tooconfigure Azure Redis 快取]: ./redis-cache/cache-configure.md
[符號中的 hello Azure Toolkit for Eclipse 指示]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
