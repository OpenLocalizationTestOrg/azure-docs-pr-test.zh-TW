---
title: "在 Azure 資料庫的 MySQL aaaServer 概念 |Microsoft 文件"
description: "本主題提供使用適用於 MySQL 之 Azure 資料庫伺服器的考量和指導方針。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a>適用於 MySQL 的 Azure 資料庫中的伺服器概念
本主題提供使用適用於 MySQL 之 Azure 資料庫伺服器的考量和指導方針。

## <a name="what-is-an-azure-database-for-mysql-server"></a>什麼是適用於 MySQL 的 Azure 資料庫伺服器？

適用於 MySQL 的 Azure 資料庫伺服器是多個資料庫的中央管理點。 它是 hello 相同就可以熟悉 hello 在內部部署的世界中的 MySQL server 建構。 具體來說，hello Azure 資料庫的 MySQL 服務管理、 提供效能保證，公開存取與伺服器層級的功能。

適用於 MySQL 的 Azure 資料庫伺服器：

- 建立於 Azure 訂用帳戶內。
- 是 hello 父資源的資料庫。
- 可為資料庫提供命名空間。
- 是一個容器具有強式存留期語意-刪除伺服器，並在刪除 hello 自主資料庫。
- 在一個區域中共置資源。
- 提供用來存取伺服器和資料庫的連接端點。
- 提供適用於 tooits 資料庫的管理原則的 hello 範圍： 登入、 防火牆、 使用者、 角色、 設定等。
- 可在多個版本中使用。 如需詳細資訊，請參閱[支援適用於 MySQL 之 Azure 資料庫的資料庫版本](./concepts-supported-versions.md)。

在適用於 MySQL Server 的 Azure 資料庫內，您可以建立一個或多個資料庫。 您可以選擇單一資料庫，每個伺服器 tooutilize toocreate 所有 hello 資源，或建立多個資料庫 tooshare hello 資源。 hello 定價是結構化的每個伺服器，根據 hello 組態的定價層，計算單位，儲存體 (GB)。 如需詳細資訊，請參閱[定價層](./concepts-service-tiers.md)。

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a>如何連接和驗證 tooan Azure 資料庫的 MySQL 伺服器嗎？

hello 下列項目有助於確保安全存取 tooyour 資料庫。

|||
| :-- | :-- |
| **驗證和授權** | 適用於 MySQL 的 Azure 資料庫伺服器支援原生的 MySQL 驗證。 您可以連接和驗證 tooserver 與 hello 伺服器系統管理員登入。 |
| **通訊協定** | hello 服務支援 MySQL 所使用的訊息架構通訊協定。 |
| **TCP/IP** | 透過 TCP/IP，並透過 Unix 網域通訊端支援 hello 通訊協定。 |
| **防火牆** | toohelp 保護您的資料、 防火牆規則可防止所有存取 tooyour 資料庫伺服器，或 tooits 資料庫，您必須先指定哪些電腦有權限。 請參閱[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)。 |
| **SSL** | hello 服務支援強制執行您的應用程式和資料庫伺服器之間的 SSL 連線。  請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。 |
|||

## <a name="how-do-i-manage-a-server"></a>如何管理伺服器？
您可以使用 Azure 入口網站 hello Azure 資料庫管理 MySQL 伺服器或 hello Azure CLI。

## <a name="next-steps"></a>後續步驟
- 如需 hello 服務的概觀，請參閱[Azure 資料庫的 MySQL 概觀](./overview.md)
- 如需以您**服務層**為依據之特定資源配額和限制的相關資訊，請參閱[服務層](./concepts-service-tiers.md)
- 如需連接 toohello 服務的資訊，請參閱[MySQL 的 Azure 資料庫的連接程式庫](./concepts-connection-libraries.md)。
