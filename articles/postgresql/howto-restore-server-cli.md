---
title: "如何 tooback 及 PostgreSQL 還原 Azure 資料庫中的伺服器 |Microsoft 文件"
description: "了解如何向上 tooback 和還原 Azure 資料庫中的伺服器為 PostgreSQL 使用 hello Azure CLI。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>向上 tooback 和還原 Azure 資料庫中的伺服器為 PostgreSQL 使用 hello Azure CLI

使用 PostgreSQL toorestore 伺服器資料庫 tooan 較早的日期，從 7 too35 天跨越 Azure 資料庫。

## <a name="prerequisites"></a>必要條件
toocomplete 此如何 tooguide，您需要：
- [「適用於 PostgreSQL 的 Azure 資料庫」伺服器和資料庫](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> 如果您安裝並在本機使用 Azure CLI hello，此方式 tooguide 會要求您使用 Azure CLI 2.0 或更新版本。 tooconfirm hello 版本，在 hello Azure CLI 命令提示字元中輸入`az --version`。 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。

## <a name="back-up-happens-automatically"></a>備份會自動進行
當您使用 Azure 資料庫進行 PostgreSQL 時，hello 資料庫服務會自動將 hello 服務的備份每隔 5 分鐘。 

基本層，hello 備份皆可為 7 天。 標準層，hello 備份皆可為 35 天。 如需詳細資訊，請參閱 [PostgreSQL 的 Azure 資料庫定價層](concepts-service-tiers.md)。

使用這個自動備份功能，您可以還原 hello 伺服器和其資料庫 tooan 早的日期或時間點。

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>還原資料庫 tooa 前一個點的時間，使用 Azure CLI hello
使用 Azure 資料庫 PostgreSQL toorestore hello 伺服器 tooa 先前時間點。 hello 還原資料複製的 tooa 新的伺服器，以及 hello 現有的伺服器保持原狀。 例如，如果卸除資料表時不小心正午今天，您可以還原 toohello 正午之前的時間。 然後，您可以擷取遺失的資料表與資料，從還原的 hello 份 hello 伺服器 hello。 

toorestore hello 伺服器，使用 hello Azure CLI [az postgres 伺服器還原](/cli/azure/postgres/server#restore)命令。

### <a name="run-hello-restore-command"></a>執行 hello restore 命令

toorestore hello 伺服器 hello Azure CLI 命令提示字元，輸入下列命令的 hello:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

hello`az postgres server restore`命令需要 hello 下列參數：
| 設定 | 建議的值 | 說明  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  Hello 來源伺服器所在的資源群組。  |
| 名稱 | mypgserver-restored | hello hello hello restore 命令所建立的新伺服器名稱。 |
| restore-point-in-time | 2017-04-13T13:59:00Z | 在時間 toorestore 至選取的點。 這個日期和時間必須在 hello 來源伺服器的備份保留期限內。 使用 hello ISO8601 日期和時間格式。 例如，您可以使用自己的當地時區，例如 `2017-04-13T05:59:00-08:00`。 您也可以使用 UTC Zulu 格式，例如 hello `2017-04-13T13:59:00Z`。 |
| source-server | mypgserver-20170401 | hello 名稱或識別碼 hello 來源伺服器 toorestore 從。 |

當您還原伺服器 tooan 早的時間點，建立新的伺服器。 hello 原始伺服器和資料庫 hello 從指定的時間點複製的 toohello 新的伺服器。

hello 位置] 和 [定價層的值為 hello 還原伺服器保持 hello 相同為 hello 原始伺服器。 

hello`az postgres server restore`是同步的命令。 還原 hello 伺服器之後，您可以使用它再次 toorepeat hello 程序的不同點的時間。 

Hello 之後還原程序完成，找出 hello 新伺服器，並確認 hello 資料還原如預期般。

## <a name="next-steps"></a>後續步驟
[「適用於 PostgreSQL 的 Azure 資料庫」的連線庫](concepts-connection-libraries.md)
