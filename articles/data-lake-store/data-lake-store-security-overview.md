---
title: "資料湖存放區中的安全性 aaaOverview |Microsoft 文件"
description: "了解 Azure Data Lake Store 如何成為更安全的巨量資料存放區"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Azure Data Lake Store 安全性
許多企業便運用商務 insights toohelp 它們進行智慧決策的巨量資料分析。 但企業的環境可能既複雜又受到規範，並且還有數目日益增加的各類使用者。 很重要的企業 toomake 確定重要商業資料更安全地儲存的 hello 正確 tooindividual 使用者授與的存取層級。 設計 azure Data Lake Store toohelp 符合這些安全性需求。 在本文中，了解 hello 安全性功能的資料湖存放區，包括：

* 驗證
* 授權
* 網路隔離
* 資料保護
* 稽核

## <a name="authentication-and-identity-management"></a>驗證和識別管理
驗證是用 hello 使用者互動資料湖存放區或任何連線 tooData 湖存放區的服務時，驗證使用者的身分識別的 hello 程序。 身分識別管理和驗證，使用 Data Lake Store [Azure Active Directory](../active-directory/active-directory-whatis.md)，完整身分識別和存取管理雲端方案，可簡化 hello 管理使用者和群組。

每個 Azure 訂用帳戶都可與 Azure Active Directory 的執行個體相關聯。 只有使用者和 Azure Active Directory 服務中定義的服務身分識別可以存取您的 Data Lake Store 帳戶使用 hello Azure 入口網站中，命令列工具，或透過您的組織是使用 hello Azure 資料的用戶端應用程式Lake Store SDK。 使用 Azure Active Directory 做為集中式存取控制機制的主要優點如下︰

* 簡化的身分識別生命週期管理。 可以快速地建立並快速撤銷只刪除或停用 hello 目錄中的 hello 帳戶 hello 身分識別的使用者或服務 （服務主體身分識別）。
* 多因素驗證。 [Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) 可為使用者登入和交易提供額外的安全性。
* 可透過標準的開放通訊協定 (例如 OAuth 或 OpenID) 從任何用戶端進行驗證。
* 可與企業目錄服務和雲端識別提供者同盟。

## <a name="authorization-and-access-control"></a>授權和存取控制
Azure Active Directory 驗證使用者，使 hello 使用者可以存取 Azure 資料湖存放區之後，授權控制項存取資料湖存放區的權限。 Data Lake Store 分隔授權帳戶相關和資料相關的活動，以下列方式 hello:

* [角色型存取控制](../active-directory/role-based-access-control-what-is.md) (RBAC)
* POSIX ACL 存取 hello 存放區中的資料

### <a name="rbac-for-account-management"></a>用於帳戶管理的 RBAC
預設會為 Data Lake Store 定義四種基本角色。 hello 角色允許透過 hello Azure 入口網站、 PowerShell cmdlet 和 REST Api 的 Data Lake Store 帳戶不同的作業。 hello 擁有者和參與者角色可以 hello 帳戶來執行各種管理功能。 您可以指派 hello 讀取器角色 toousers 人員只能與資料互動。

![RBAC 角色](./media/data-lake-store-security-overview/rbac-roles.png "RBAC 角色")

請注意，雖然角色指派帳戶管理，一些角色會影響存取 toodata。 您需要 toouse Acl toocontrol 存取 toooperations 使用者可以在 hello 檔案系統上執行。 下表中的 hello 顯示管理權利與 hello 的資料存取權限的摘要預設角色。

| 角色 | 管理權限 | 資料存取權限 | 說明 |
| --- | --- | --- | --- |
| 未指派角色 |None |由 ACL 控管 |hello 使用者無法使用 hello Azure 入口網站或 Azure PowerShell cmdlet toobrowse 資料湖存放區。 hello 使用者可以使用命令列工具。 |
| 擁有者 |全部 |全部 |hello 擁有者角色是超級使用者。 此角色可管理的所有項目，且具有完整存取 toodata。 |
| 讀取者 |唯讀 |由 ACL 控管 |hello 讀取者角色可以檢視關於帳戶的管理，例如其中使用者會獲指派 toowhich 角色的所有項目。 hello 讀取者角色無法進行任何變更。 |
| 參與者 |除了新增和移除角色以外的一切 |由 ACL 控管 |hello 參與者角色可管理的帳戶，例如部署以及建立及管理警示的某些層面。 hello 參與者角色無法加入或移除角色。 |
| 使用者存取系統管理員 |新增和移除角色 |由 ACL 控管 |hello 使用者存取系統管理員角色可以管理使用者存取 tooaccounts。 |

如需指示，請參閱[指派使用者或安全性群組 tooData Lake Store 帳戶](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts)。

### <a name="using-acls-for-operations-on-file-systems"></a>在檔案系統上使用 ACL 執行作業
Data Lake Store 是 Hadoop 分散式檔案系統 (HDFS) 之類的階層式檔案系統，並可支援 [POSIX ACL](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists)。 它可控制讀取 (r)、 寫入 (w) 及執行 (x) 的權限 tooresources hello 擁有者角色、 hello 擁有者群組，以及其他使用者和群組。 Hello 資料湖存放區公開預覽版 （hello 目前版本），Acl 可以啟用 hello 根資料夾、 子資料夾和個別檔案。 如需 ACL 如何在 Data Lake Store 的內容中運作的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。

建議您使用 [安全性群組](../active-directory/active-directory-accessmanagement-manage-groups.md)為多個使用者定義 ACL。 新增使用者 tooa 安全性群組，並再將指派的檔案或資料夾 toothat 安全性群組的 hello Acl。 這非常有用當您想要 tooprovide 自訂存取，因為您是有限的 tooadding 最多 9 個自訂存取項目。 如需如何 toobetter 安全資料儲存在資料湖存放區中，使用 Azure Active Directory 安全性群組的詳細資訊，請參閱[將使用者或安全性群組指派為 Azure Data Lake Store 檔案系統的 Acl toohello](data-lake-store-secure-data.md#filepermissions)。

![列出標準和自訂存取](./media/data-lake-store-security-overview/adl.acl.2.png "列出標準和自訂的存取")

## <a name="network-isolation"></a>網路隔離
使用 Data Lake Store toohelp 控制存取 tooyour 資料儲存在 hello 網路層級。 您可以建立防火牆，並且為受信任的用戶端定義 IP 位址範圍。 使用 IP 位址範圍，只有具有 hello 定義範圍內的 IP 位址的用戶端連線 tooData 湖存放區。

![防火牆設定和 IP 存取](./media/data-lake-store-security-overview/firewall-ip-access.png "防火牆設定和 IP 位址")

## <a name="data-protection"></a>資料保護
Azure Data Lake Store 在資料的生命週期中保護您的資料。 資料在傳輸過程中，資料湖存放區會使用 hello 業界標準的傳輸層安全性 (TLS) 通訊協定 toosecure 資料 hello 網路上。

![Data Lake Store 中的加密](./media/data-lake-store-security-overview/adls-encryption.png "Data Lake Store 中的加密")

資料湖存放區也提供儲存在 hello 帳戶中的資料加密。 您可以選擇 toohave 加密資料，或選擇不使用加密。 如果您選擇進行加密，資料湖存放區中儲存的資料是持續性的媒體上的加密之前 toostoring。 在這種情況下，資料湖存放區會自動加密資料的先前 toopersisting 和解密先前 tooretrieval 資料，因此它是完全透明 toohello 用戶端存取 hello 資料。 沒有任何程式碼變更，需要在 hello 用戶端 tooencrypt/解密資料。

金鑰管理，資料湖存放區會用於管理您所需的解密儲存在 hello 資料湖存放區中的任何資料的主要加密金鑰 (MEKs)，提供兩種模式。 您可以讓資料湖存放區 hello MEKs 管理，或選擇使用 Azure 金鑰保存庫帳戶 hello MEKs tooretain 擁有權。 您的金鑰管理的 hello 模式時在建立時指定的 Data Lake Store 帳戶。 如需有關如何 tooprovide 加密相關的組態，請參閱[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](data-lake-store-get-started-portal.md)。

## <a name="auditing-and-diagnostic-logs"></a>稽核和診斷記錄檔
您可以視您要尋找管理相關活動或資料相關活動的記錄檔而定，使用稽核或診斷記錄檔。

* 使用 Azure 資源管理員 Api 並透過稽核記錄檔會顯示 hello Azure 入口網站中管理相關的活動。
* 與資料相關的活動使用 WebHDFS REST Api，並透過診斷記錄檔會顯示 hello Azure 入口網站中。

### <a name="auditing-logs"></a>稽核記錄檔
toocomply 的規定，組織可能需要適當的稽核記錄 toodig，需要為特定的事件。 Data Lake Store 有內建的監視和稽核作業，並且會記錄所有的帳戶管理活動。

帳戶管理稽核記錄，檢視並選擇 hello 資料行的 toolog。 您也可以匯出稽核記錄檔 tooAzure 儲存體。

![稽核記錄](./media/data-lake-store-security-overview/audit-logs.png "稽核記錄")

### <a name="diagnostic-logs"></a>診斷記錄檔
您可以在 hello （在診斷的設定） 的 Azure 入口網站中設定資料存取稽核記錄，並建立 hello 記錄檔的儲存位置的 Azure Blob 儲存體帳戶。

![診斷記錄檔](./media/data-lake-store-security-overview/diagnostic-logs.png "診斷記錄檔")

設定診斷設定之後，您可以檢視 hello 記錄檔上 hello**診斷記錄檔** 索引標籤。

如需使用 Azure Data Lake Store 診斷記錄檔的詳細資訊，請參閱 [存取 Data Lake Store 的診斷記錄檔](data-lake-store-diagnostic-logs.md)。

## <a name="summary"></a>摘要
企業客戶要求是安全又簡單 toouse 資料分析雲端平台。 設計 azure Data Lake Store toohelp 滿足下列需求，透過身分識別管理及驗證透過 Azure Active Directory 整合、 ACL 為基礎的授權、 網路隔離、 資料加密傳輸中和靜止 （傳入 hello未來），以及稽核。

如果您想 toosee 資料湖存放區中的新功能，傳送給我們意見反應在 hello[資料湖存放區 UserVoice 論壇](https://feedback.azure.com/forums/327234-data-lake)。

## <a name="see-also"></a>另請參閱
* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
* [開始使用 Data Lake Store](data-lake-store-get-started-portal.md)
* [保護 Data Lake Store 中的資料](data-lake-store-secure-data.md)

