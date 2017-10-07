---
title: "aaaCreate 傳統的 Azure VM 執行 MySQL |Microsoft 文件"
description: "建立 Azure 虛擬機器執行 Windows Server 2012 R2 和 hello 使用 hello 傳統部署模型的 MySQL 資料庫。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>在執行 Windows Server 2016 的 hello 傳統部署模型所建立的虛擬機器上安裝 MySQL
[MySQL](https://www.mysql.com) 是一種很受歡迎的開放原始碼 SQL 資料庫。 本教學課程示範如何 tooinstall 和執行 hello**社群版本的 MySQL 5.7.18**為 MySQL 伺服器上執行的虛擬機器**Windows Server 2016**。 對於非 MySQL 或 Windows Server 的版本，操作方式可能略有不同。

如需 MySQL 安裝在 Linux 上的指示，請參閱：[如何在 Azure 上 MySQL tooinstall](../../linux/mysql-install.md)。

> [!IMPORTANT]
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>建立執行 Windows Server 2016 的虛擬機器
如果您還沒有執行 Windows Server 2016 的 VM，您可以使用這個[教學課程](./tutorial.md)toocreate hello 虛擬機器。

## <a name="attach-a-data-disk"></a>連接資料磁碟
Hello 虛擬機器建立之後，您可以選擇性地附加資料磁碟。 新增資料磁碟建議用於生產工作負載和 tooavoid hello 作業系統磁碟機 （c:） 上的空間用盡，包括 hello 作業系統。

請參閱[tooattach 資料磁碟 tooa Windows 虛擬機器如何](../attach-managed-disk-portal.md)依照 hello 指示連接空磁碟。 設定 hello 主機快取設定太**無**或**唯讀**。

## <a name="log-on-toohello-virtual-machine"></a>登入 toohello 虛擬機器
接下來，您將[登入 toohello 虛擬機器](./connect-logon.md)，才能安裝 MySQL。

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>安裝並執行 hello 虛擬機器上的 MySQL Community 伺服器
請遵循這些步驟 tooinstall、 設定及執行的 MySQL Server hello 社群版本：

> [!NOTE]
> 當下載使用 Internet Explorer 的項目，您可以設定 hello IE**增強式安全性設定**tooOff，並簡化 hello 下載程序。 從 hello 開始 功能表，按一下 系統管理工具/伺服器管理員/本機伺服器，然後按一下 IE**增強式安全性設定**並設定 hello 組態 tooOff)。
>
>

1. 您已連接 toohello 虛擬機器使用遠端桌面之後，請按一下**Internet Explorer**從 hello [開始] 畫面。
2. 選取 hello**工具**按鈕在 hello 右上角 （hello cogged 的滾輪圖示），然後按一下**網際網路選項**。 按一下 hello**安全性**索引標籤上，按一下 hello**信任的網站**圖示，然後按一下hello**網站** 按鈕。 新增信任的網站 http://*.mysql.com toohello 清單。 按一下 關閉，然後按一下確定。
3. 在 hello 位址列的 Internet Explorer 中，輸入 https://dev.mysql.com/downloads/mysql/。
4. 使用 hello MySQL 網站 toolocate 並下載 hello hello MySQL Windows 安裝程式最新版本。 在選擇 hello MySQL 安裝程式時，下載已完成檔案組 (例如，hello mysql-安裝程式-社群-5.7.18.0.msi 352.8 MB 的檔案大小)，並儲存 hello installer hello 的 hello 版本。
5. 當下載完成 hello 安裝程式之後時，按一下 **執行**toolaunch 安裝程式。
6. 在 hello**合約**頁面上，接受 hello 授權合約，然後按一下**下一步**。
7. 在 hello**選擇安裝類型**頁面上，按一下 hello 安裝類型，然後再按一下**下一步**。 hello 下列步驟假設 hello 選取範圍的 hello**僅限伺服器**安裝類型。
8. 如果 hello**檢查需求**顯示頁面上，按一下**Execute** toolet hello 安裝程式會安裝任何遺漏的元件。 請遵循顯示，例如 hello c + + 可轉散發套件的執行階段的任何指示。
9. 在 hello**安裝**頁面上，按一下**Execute**。 安裝完成時，按 [下一步] 。

10. 在 hello**產品組態**頁面上，按一下**下一步**。

11. 在 hello**類型和網路**頁面上，指定所需的組態類型和連接選項，包括 hello TCP 連接埠，如有需要。 選取 [顯示進階選項]，然後按 [下一步]。
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. 在 hello**帳戶和角色**頁面上，指定強式 MySQL 根密碼。 視需要新增其他 MySQL 使用者帳戶，然後按 [下一步] 。

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. 在 hello **Windows 服務**頁面上，執行 hello MySQL 伺服器當做 Windows 服務，如有需要指定變更 toohello 預設設定，然後按一下**下一步**。

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. hello hello 上的選擇**增益集和擴充功能**是選擇性的頁面。 按一下**下一步**toocontinue。
15. 在 hello**進階選項**頁面上，視需要指定變更 toologging 選項，然後按一下**下一步**。

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. 在 hello**套用伺服器設定**頁面上，按一下**Execute**。 Hello 組態步驟完成時，按一下**完成**。
17. 在 hello**產品組態**頁面上，按一下**下一步**。
18. 在 hello**安裝完成**頁面上，按一下**複製記錄 tooClipboard**如果它在更新版本中，然後再按一下想要 tooexamine**完成**。
19. 從 hello [開始] 畫面，輸入**mysql**，然後按一下 **MySQL 5.7 命令列用戶端**。
20. 輸入您在步驟 12 中指定的 hello 根密碼，然後您會看到提示，您可以在其中發出命令 tooconfigure MySQL。 Hello 命令和語法的詳細資訊，請參閱[MySQL 參考手冊](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html)。

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. 您也可以設定伺服器預設設定，例如基底 hello 和資料目錄以及磁碟機。 如需詳細資訊，請參閱 [6.1.2 伺服器組態預設值](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html)。

## <a name="configure-endpoints"></a>設定端點

Hello MySQL 服務 toobe 可用 tooclient 電腦 hello 網際網路上，您必須設定 hello TCP 連接埠的端點，並建立 Windows 防火牆規則。 hello 的 hello MySQL Server 服務所接聽的 MySQL 用戶端的預設通訊埠值為 3306。 您可以指定另一個連接埠，只要 hello 連接埠與 hello hello 上提供的值一致**類型和網路**頁面 （hello 上一個程序的步驟 11）。

> [!NOTE]
> 用於實際執行環境，請考慮讓 hello MySQL 伺服器 hello 網際網路上的服務可用 tooall 電腦的安全性含意 hello。 您可以定義 hello 組允許 toouse hello 端點的存取控制清單 (ACL) 的來源 IP 位址。 如需詳細資訊，請參閱[如何 tooSet 端點 tooa 虛擬機器](setup-endpoints.md)。
>
>

tooconfigure hello MySQL Server 服務的端點：

1. 在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**，按一下 MySQL 虛擬機器的 hello 名稱，然後按一下**端點**。
2. Hello 命令列中，按一下 **新增**。
3. 在 hello**加入端點**頁面上，輸入唯一的名稱**名稱**。
4. 選取**TCP**做為 hello 通訊協定。
5. 輸入 hello 通訊埠編號，例如**3306**，在這兩**公用連接埠**和**私用連接埠**，然後按一下**確定**。

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>加入 Windows 防火牆規則 tooallow MySQL 流量
Windows 防火牆規則，允許從 hello 網際網路上，執行下列命令在 hello MySQL 流量 tooadd_提升權限的 Windows PowerShell 命令提示字元_hello MySQL server 虛擬機器上。

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>測試您的遠端連線
tootest 您遠端連線 toohello Azure VM 執行 hello MySQL 伺服器服務，您必須提供 hello 包含 hello VN hello 雲端服務 DNS 名稱。

1. 在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**，按一下 MySQL server 虛擬機器，hello 名稱，然後按一下**概觀**。
2. 從 hello 虛擬機器儀表板，請注意 hello **DNS 名稱**值。 下列是一個範例：

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. 從本機電腦上執行的 MySQL 或 hello MySQL 用戶端，執行下列中的 MySQL 使用者身分的命令 toolog hello。

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   例如，使用 hello MySQL 使用者名稱_dbadmin3_和 hello _testmysql.cloudapp.net_ DNS 名稱 hello 虛擬機器，您可以開始使用下列命令的 hello MySQL:

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>後續步驟
toolearn 有關執行 MySQL 的詳細資訊，請參閱 「 hello [MySQL 文件](http://dev.mysql.com/doc/)。
