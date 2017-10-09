---
title: "aaaAzure 資料庫的 MySQL 伺服器防火牆規則 |Microsoft 文件"
description: "描述適用於 MySQL 的 Azure 資料庫伺服器防火牆規則。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1f85310385da947b6c492aa6aa21c1b885c2a97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a>適用於 MySQL 的 Azure 資料庫伺服器防火牆規則
防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。 hello 防火牆會授與存取 toohello 伺服器 hello 來自每個要求的 IP 位址為基礎。

tooconfigure 防火牆，您會建立指定的可接受的 IP 位址範圍的防火牆規則。 您可以在 hello 伺服器層級建立防火牆規則。

**防火牆規則：**這些規則可讓用戶端 tooaccess 整個 Azure 資料庫的 MySQL server，也就是所有都 hello 資料庫都 hello 相同邏輯伺服器。 藉由使用 hello Azure 入口網站，或使用 Azure CLI 命令，可以設定伺服器層級防火牆規則。 toocreate 伺服器層級防火牆規則，您必須是 hello 訂用帳戶擁有者或訂閱參與者。

## <a name="firewall-overview"></a>防火牆概觀
Hello 防火牆封鎖 MySQL 伺服器的所有資料庫存取 tooyour Azure 資料庫的預設值。 toobegin 使用您的伺服器從另一部電腦，您需要 toospecify 其中一個或多伺服器層級防火牆規則 tooenable 存取 tooyour 伺服器。 使用的 IP 位址範圍是從 hello 網際網路 tooallow hello 防火牆規則 toospecify。 存取 toohello Azure 入口網站本身不會受到 hello 防火牆規則。

從連線嘗試 hello 網際網路和 Azure 必須先通過 hello 防火牆才能到達您的 Azure 資料庫的 MySQL 資料庫，如下列圖表中的 hello 中所示：

![範例流程的 hello 防火牆的運作方式](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a>從 hello 網際網路連線
伺服器層級防火牆規則套用 tooall 資料庫上的 MySQL 伺服器 hello Azure 資料庫。

如果 hello 要求 hello IP 位址是其中一個 hello hello 伺服器層級防火牆規則中指定的範圍內，會授與 hello 連線。

如果 hello 要求 hello IP 位址不在任何 hello 資料庫層級中指定 hello 範圍或伺服器層級防火牆規則，hello 連接要求會失敗。

## <a name="programmatically-managing-firewall-rules"></a>以程式設計方式管理防火牆規則
除了以程式設計方式使用 Azure CLI toohello Azure 入口網站中，防火牆規則可以是所管理。 另請參閱[使用 Azure CLI 建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則](./howto-manage-firewall-using-cli.md)

## <a name="troubleshooting-hello-database-firewall"></a>疑難排解 hello database 防火牆
請考慮 hello 時存取 toohello Microsoft Azure 資料庫的 MySQL server 服務未如預期般運作，下列點：

* **變更 toohello 允許清單有尚未生效：**可能會如往常般的五分鐘延遲變更 MySQL 伺服器的防火牆組態 tootake 效果 toohello Azure 資料庫。

* **hello 登入未獲授權，或使用不正確的密碼：**登入沒有權限 hello Azure 資料庫上使用的 MySQL 伺服器或 hello 密碼不正確，如果 hello 連接 toohello Azure 資料庫的 MySQL 伺服器遭拒。 建立防火牆設定只提供連接 tooyour 伺服器; 機會 tooattempt 用戶端每個用戶端必須提供 hello 必要的安全性認證。

* **動態 IP 位址：**如果您有使用動態 IP 位址的網際網路連線，並且在經由 hello 防火牆時遇到，您可以嘗試下列解決方案 hello 的其中一個：

* 要求網際網路服務提供者 (ISP) hello IP 位址範圍指派 tooyour 用戶端電腦的 MySQL server，該存取 hello Azure 資料庫，然後將 hello IP 位址範圍新增為防火牆規則。

* 取得靜態 IP 位址改為您的用戶端電腦，然後將 hello IP 位址新增為防火牆規則。

## <a name="next-steps"></a>後續步驟

[建立和管理 MySQL 防火牆規則使用 hello Azure 入口網站的 Azure 資料庫](./howto-manage-firewall-using-portal.md)
[建立及管理 Azure 資料庫使用 Azure CLI MySQL 防火牆規則](./howto-manage-firewall-using-cli.md)
