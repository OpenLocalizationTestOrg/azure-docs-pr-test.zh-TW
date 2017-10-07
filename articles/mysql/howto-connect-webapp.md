---
title: "現有 Azure App Service tooAzure aaaConnect MySQL 資料庫 |Microsoft 文件"
description: "指示如何 tooproperly 連接現有的 Azure App Service tooAzure 資料庫的 MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a>連接 [MySQL 伺服器的現有 Azure App Service tooAzure 資料庫
本文件說明如何 tooconnect 現有的 Azure App Service tooyour Azure 資料庫的 MySQL 伺服器。

## <a name="before-you-begin"></a>開始之前
登入 toohello [Azure 入口網站](https://portal.azure.com)。 建立適用於 MySQL 伺服器的 Azure 資料庫。 如需詳細資訊，請參閱太[如何從入口網站的 MySQL 伺服器資料庫的 toocreate Azure](quickstart-create-mysql-server-database-using-azure-portal.md)或[如何 toocreate Azure 資料庫的 MySQL 伺服器使用 CLI](quickstart-create-mysql-server-database-using-azure-cli.md)。

目前有兩個方案 tooenable Azure App Service tooan Azure 資料庫存取的權限 MySQL。 這兩種解決方案都需要設定伺服器層級防火牆規則。

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a>解決方案 1-建立防火牆規則 tooallow 所有 Ip
Azure 的 MySQL 資料庫提供使用防火牆 tooprotect 您資料的存取安全性。 時從 MySQL 伺服器的 Azure App Service tooAzure 資料庫連接記住該 hello 輸出應用程式服務的 Ip 是動態的本質。 

tooensure hello 可用性，您的 Azure 應用程式服務，我們建議使用此方案 tooallow 所有 Ip。

> [!NOTE]
> Microsoft 正在為長期的方案 tooavoid MySQL 允許 Azure 服務 tooconnect tooAzure 資料庫的所有 Ip。

1. Hello MySQL 伺服器] 刀鋒視窗，設定下標題之下，按一下**連線安全性**tooopen hello 連線安全性刀鋒視窗中的 hello Azure MySQL 資料庫。

   ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. 輸入 [規則名稱]、[起始 IP] 和 [結束 IP]。 然後按一下 [儲存] 。
   - 規則名稱：允許所有 IP
   - 起始 IP：0.0.0.0
   - 結束 IP：255.255.255.255

   ![Azure 入口網站 - 新增所有 IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a>解決方案 2-建立防火牆規則 tooexplicitly 允許輸出 Ip
您可以明確加入所有 hello 輸出 Ip，您的 Azure 應用程式服務。

1. 在 [hello 應用程式服務的屬性刀鋒視窗中，檢視您**輸出的 IP 位址**。

   ![Azure 入口網站 - 檢視輸出 IP](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. 在 hello MySQL 連線安全性刀鋒視窗中，新增一個輸出的 Ip。

   ![Azure 入口網站 - 新增明確的 IP](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. 請記住太**儲存**您的防火牆規則。

雖然 hello Azure 應用程式服務會嘗試 tookeep IP 位址常數經過一段時間，有可能會在其中變更 hello IP 位址的情況。 比方說，當 hello 應用程式回收或調整規模作業，就會發生，或在 Azure 的區域資料中加入新機器時中心 tooincrease hello 容量。 當 hello IP 位址變更時，hello 應用程式可能會停止運作，無法再連接 hello 事件中的 toohello MySQL 伺服器。 選擇 hello 前面解決方案的其中一個時，請考慮此可能性。

## <a name="ssl-configuration"></a>SSL 設定
適用於 MySQL 的 Azure 資料庫預設會啟用 SSL。 如果您的應用程式不使用 SSL tooconnect toohello 資料庫，您需要 toodisable SSL MySQL 伺服器上。 如需詳細資訊，如何 tooconfigure SSL，請參閱[使用 SSL 與 Azure 資料庫的 MySQL](howto-configure-ssl.md)。

## <a name="next-steps"></a>後續步驟
如需有關連接字串的詳細資訊，請參閱太[連接字串](howto-connection-string.md)。
