---
title: "適用於 MySQL 的 Azure 資料庫的 SSL 連線能力 | Microsoft Docs"
description: "用以設定適用於 MySQL 之 Azure 資料庫及相關聯應用程式以適當使用 SSL 連接的資訊"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 11/02/2017
ms.openlocfilehash: 37e2bbbe1ed4b6a9cca0e0b001e5e632b9b73be2
ms.sourcegitcommit: 3df3fcec9ac9e56a3f5282f6c65e5a9bc1b5ba22
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a>適用於 MySQL 的 Azure 資料庫中的 SSL 連線能力
適用於 MySQL 的 Azure 資料庫支援使用安全通訊端層 (SSL)，將資料庫伺服器連接至用戶端應用程式。 在您的資料庫伺服器和用戶端應用程式之間強制執行 SSL 連接，有助於藉由將伺服器與您應用程式之間的資料流加密，來提供保護以抵禦「中間人」攻擊。

## <a name="default-settings"></a>預設設定
根據預設，資料庫服務應該會設定為在連接至 MySQL時需要 SSL 連接。  建議盡可能地避免停用 SSL 選項。 

透過 Azure 入口網站和 CLI 佈建新的適用於 MySQL 的 Azure 資料庫伺服器時，預設會強制執行 SSL 連接。 

Azure 入口網站中會顯示多種程式設計語言的連接字串。 這些連接字串包含連接到您資料庫所需的 SSL 參數。 在 Azure 入口網站中選取您的伺服器。 在下 [設定] 標題之下，選取 [連接字串]。 SSL 參數會根據連接器而有所不同，例如，"ssl=true" 或 "sslmode=require" 或 "sslmode=required" 及其他變化。

若要了解如何在開發應用程式時啟用或停用 SSL 連接，請參閱[如何設定 SSL](howto-configure-ssl.md)。 

## <a name="next-steps"></a>後續步驟
[適用於 MySQL 的 Azure 資料庫的連線庫](concepts-connection-libraries.md)
