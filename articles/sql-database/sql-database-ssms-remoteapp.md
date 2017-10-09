---
title: "aaaConnect tooSQL Azure RemoteApp 中使用 SQL Server Management Studio 的資料庫 |Microsoft 文件"
description: "如何使用這個教學課程 toolearn toouse Azure RemoteApp 中的 SQL Server Management Studio 的安全性和連接 tooSQL 資料庫時的效能"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>在 Azure RemoteApp tooconnect tooSQL 資料庫中使用 SQL Server Management Studio

> [!IMPORTANT]
> Azure RemoteApp 即將中止。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
>

## <a name="introduction"></a>簡介
本教學課程示範如何在 Azure RemoteApp tooconnect tooSQL 資料庫 toouse SQL Server Management Studio (SSMS)。 它會引導您設定 SQL Server Management Studio，在 Azure RemoteApp 中的 hello 程序、 說明 hello 優點，並顯示安全性功能，您可以使用 Azure Active Directory 中。

**估計時間 toocomplete:** 45 分鐘的時間

## <a name="ssms-in-azure-remoteapp"></a>Azure RemoteApp 中的 SSMS
Azure RemoteApp 是在 Azure 中的一項 RDS 服務，可提供應用程式。 您可以在此處深入了解： [什麼是 RemoteApp？](../remoteapp/remoteapp-whatis.md)

SSMS 執行在 Azure RemoteApp 可讓您 hello 與在本機執行 SSMS 相同的體驗。

![螢幕擷取畫面顯示正在 Azure RemoteApp 中執行的 SSMS][1]

## <a name="benefits"></a>優點
有許多優點 toousing Azure RemoteApp 中的 SSMS 包括：

* Azure SQL server 上的通訊埠 1433年沒有 toobe 公開外部 （Azure) 外部。
* 不是需要 tookeep 新增和移除 hello Azure SQL server 防火牆中的 IP 位址。
* 所有 Azure RemoteApp 連線都會使用加密的遠端桌面通訊協定，透過 HTTPS 在連接埠 443 上進行
* 這是多使用者功能，且可以調整。
* 不必 SSMS hello 效能提升 hello SQL 資料庫與相同的區域。
* 您可以稽核 hello Premium edition，其具有使用者活動報告的 Azure Active directory 與 Azure remoteapp 使用。
* 您可以啟用 Multi-Factor Authentication (MFA)。
* 存取任何地方時使用任何 hello SSMS 支援的 Azure RemoteApp 用戶端，包括 iOS、 Android、 Mac、 Windows Phone 和 Windows 電腦。

## <a name="create-hello-azure-remoteapp-collection"></a>建立 hello Azure RemoteApp 集合
以下是您的 Azure RemoteApp 集合，使用 SSMS hello 步驟 toocreate:

### <a name="1-create-a-new-windows-vm-from-image"></a>1.從映像建立新的 Windows VM
新的 VM 使用 hello hello 圖庫 toomake 從 「 Windows Server 遠端桌面工作階段主機 Windows Server 2012 R2 」 映像。

### <a name="2-install-ssms-from-sql-express"></a>2.從 SQL Express 安裝 SSMS
移至 hello 新的 VM，並瀏覽 toothis 下載頁面： [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

沒有選項 tooonly 下載 SSMS。 下載之後, 進入 hello 安裝目錄並執行安裝程式 tooinstall SSMS。

您也需要 tooinstall SQL Server 2014 Service Pack 1。 您可以在這裡下載：[Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

SQL Server 2014 Service Pack 1 包含和 Azure SQL Database 搭配使用的基本功能。

### <a name="3-run-validate-script-and-sysprep"></a>3.執行「驗證」指令碼和 SysPrep
Hello VM 桌面上是 hello 的稱為驗證的 PowerShell 指令碼。 按兩下以執行此指令碼。 它將會驗證該 hello VM 準備好 toobe 用於遠端裝載的應用程式。 驗證完成時，它會要求 toorun sysprep-選擇 toorun 它。

Sysprep 完成時，它會關閉 hello VM。

toolearn 進一步了解建立 Azure RemoteApp 映像，請參閱： [toocreate RemoteApp 範本映像在 Azure 中的方式](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4.擷取映像
當 VM 已停止執行，hello hello 目前入口網站中找到它和擷取它。

toolearn 深入了解擷取映像，請參閱[擷取與 hello 傳統部署模型所建立的 Azure Windows 虛擬機器的映像](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5.新增 tooAzure RemoteApp 範本映像
在 hello hello 目前入口網站的 Azure RemoteApp 區段中，移 toohello 範本映像 索引標籤並按一下 新增。 在 hello 快顯方塊中，選取 [從虛擬機器程式庫匯入映像]，然後選擇 hello 您剛才建立的映像。

### <a name="6-create-cloud-collection"></a>6.建立雲端集合
Hello 目前入口網站中建立新的 Azure RemoteApp 雲端集合。 選擇您剛才匯入使用 SSMS 在其上安裝的範本影像 hello。

![建立新的雲端集合][2]

### <a name="7-publish-ssms"></a>7.發佈 SSMS
Hello hello 從應用程式發行新的雲端集合，選取發行] 索引標籤上的 [開始] 功能表，然後從 hello 清單中選擇 [SSMS。

![發佈應用程式][5]

### <a name="8-add-users"></a>8.新增使用者
Hello 使用者存取 索引標籤中，您可以選取 hello 使用者必須存取其中只包含 SSMS toothis Azure RemoteApp 集合。

![新增使用者][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9.安裝 hello Azure RemoteApp 用戶端應用程式
您可以在這裡下載並安裝 Azure RemoteApp 用戶端： [下載 | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>設定 Azure SQL Server
hello 只需要設定了 Azure 服務的 tooensure 啟用 hello 防火牆。 如果您使用此方案，然後您不需要 tooadd 任何 IP 位址 tooopen hello 防火牆。 允許 toohello SQL Server 的 hello 網路流量會從其他 Azure 服務。

![Azure 允許][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)
可特別為此應用程式啟用 MFA。 移 toohello 的 Azure Active Directory 的應用程式 索引標籤。 您會發現 Microsoft Azure RemoteApp 的項目。 如果您按一下該應用程式，然後設定時，您會看到 hello 頁面下方，您可以啟用 MFA，此應用程式。

![啟用 MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>使用 Azure Active Directory Premium 稽核使用者活動
如果您沒有 Azure AD Premium，則必須 tooturn 它在 hello 授權您的目錄區段。 已啟用 Premium，您可以將使用者指派給 toohello Premium 層級。

當您移 tooa 使用者在 Azure Active Directory 中時，您可以前往 toohello 活動索引標籤 toosee 登入資訊 tooAzure RemoteApp。

## <a name="next-steps"></a>後續步驟
完成上述步驟的所有 hello 之後, 您將無法 toorun hello Azure RemoteApp 的用戶端與登入與指派的使用者。 您會做為其中一個應用程式提供使用 SSMS，而且它存取 tooAzure SQL server 電腦上安裝時執行它。

如需有關如何 toomake hello 連接 tooSQL 資料庫的詳細資訊，請參閱[連接 SQL Server Management Studio tooSQL 資料庫及執行範例 T-SQL 查詢](sql-database-connect-query-ssms.md)。

以上為目前的所有內容。 盡情享受！

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png