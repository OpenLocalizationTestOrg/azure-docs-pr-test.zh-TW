---
title: "在 Microsoft Azure 中的個人資料 aaaManage |Microsoft 文件"
description: "指引 toocorrect，如何更新、 刪除及匯出 Azure Active Directory 和 Azure SQL Database 中的個人資料"
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a>在 Microsoft Azure 中管理個人資料

本文提供指引 toocorrect，如何更新、 刪除及匯出 Azure Active Directory 和 Azure SQL Database 中的個人資料。

## <a name="scenario"></a>案例

Dublin 公司提供高階目的地結婚愛爾蘭及本機和國際客戶基底的 hello world 購買一次。 它們有辦公室、 客戶、 員工和廠商各地 hello world toofully 服務 hello 管道時所提供。

在許多其他項目，hello 公司會追蹤的與會者包含食物的過敏情況和飲食喜好設定。 告別來賓可以註冊的各種活動，例如有時騎馬 riding，瀏覽，船了，以此類推，與甚至彼此互動管理中心的 web 網頁上 hello 月乃至 toohello 事件期間。 hello 公司會從員工、 廠商、 客戶和場遊客收集個人資訊。 因為 hello 國際性質 hello 商務 hello 公司必須符合規定的多個層級。

## <a name="problem-statement"></a>問題陳述

- 資料的系統管理員必須能夠 toocorrect 不正確個人資訊及更新未完成或變更個人資訊。

- 資料的系統管理員需要必須能夠 toodelete 個人 hello 要求資料主體資訊。

- 資料的系統管理員需要 tooexport 資料，並提供它 tooa 資料主旨常見且結構化的格式，依據他或她的要求。

## <a name="company-goals"></a>公司目標

- 必須在 Azure Active Directory 與 Azure SQL Database 中更正或更新不正確或不完整的客戶、婚禮賓客、員工及合作廠商的個人資訊。

- 依據資料主旨 hello 要求，必須在 Azure Active Directory 和 Azure SQL Database 中刪除的個人資訊。

- 必須依據 hello 資料主體要求以通用的結構化格式匯出個人資料。

## <a name="solutions"></a>解決方案

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory：改正/更正不正確或不完整的個人資料，並清除/刪除個人資料/使用者設定檔

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) 是 Microsoft 的雲端式、多租用戶目錄和身分識別管理服務。
您可以更正、 更新或刪除客戶和員工的使用者設定檔與使用者工作資訊中包含個人資料，例如使用者名稱、 工作標題、 地址或電話號碼，您[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD)環境使用 hello [Azure 入口網站](https://portal.azure.com/)。

您必須使用屬於 hello 目錄全域管理員帳戶登入。

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>如何在 Azure Active Directory 中更正或更新使用者設定檔和工作資訊？

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。

2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

    ![media/image1.png](media/manage-personal-data-azure/image001.png)

3. 在 hello**使用者和群組**刀鋒視窗中，選取**使用者**。

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. 在 [hello**使用者和群組的使用者**刀鋒視窗中，從 [hello] 清單中，選取使用者，然後用 hello 選使用者的 hello] 刀鋒視窗，選取**設定檔**tooview hello 使用者設定檔資訊需要更正 toobe或更新。

    ![media/image3.png](media/manage-personal-data-azure/image005.png)

5. 修正或更新 hello 資訊，然後 hello 命令列中，選取**儲存。**

6.  在 hello 選使用者的 hello 刀鋒視窗，選取 **工作資訊**tooview 使用者工作的資訊需要 toobe 修正或更新。

    ![media/image4.png](media/manage-personal-data-azure/image007.png)

7. 更正或更新 hello 使用者工作的資訊，然後再，hello 命令列中，選取**儲存。**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>如何在 Azure Active Directory 中刪除使用者設定檔？

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)hello 目錄的全域管理員的帳戶。

2. 選取**更多服務**，輸入**使用者和群組**在 hello 文字方塊中，然後選取  **Enter**。

    ![](media/manage-personal-data-azure/image001.png)

3. 在 hello**使用者和群組**刀鋒視窗中，選取**使用者**。

    ![media/image2.png](media/manage-personal-data-azure/image003.png)

4. 在 hello**使用者和群組的使用者**刀鋒視窗中，選取的使用者從 hello 清單。

    ![media/image3.png](media/manage-personal-data-azure/image007.png)

5. 在 hello 選使用者的 hello 刀鋒視窗，選取 **概觀**，然後 hello 命令列中，選取**刪除**。

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>SQL Database：改正/更正不正確或不完整的個人資料；清除/刪除個人資料；匯出個人資料 

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 是雲端資料庫，可協助開發人員建置及維護應用程式。

您可以使用標準 SQL 查詢在 [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 中更新個人資料，也可將其刪除。 此外，可以從 SQL Database 使用各種不同方法，包括 hello Azure SQL Server 匯入和匯出精靈 」，並在各種不同的格式，其中包括的 BACPAC 檔案匯出個人資料。

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>如何更正、更新或清除 SQL Database 中的個人資料？

toolearn toocorrect 或更新 SQL Database 中的個人資料如何瀏覽 hello[更新 (TRANSACT-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql)，[更新文字](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql)，[更新 with 通用資料表運算式](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql)，或[更新寫入文字](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql)文件。

toolearn toodelete SQL Database 中的個人資料如何瀏覽 hello[刪除 (TRANSACT-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql)文件。

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>我要如何匯出 SQL Database 中的個人資料 tooa BACPAC 檔案？

BACPAC 檔案包含 hello SQL 資料庫資料和中繼資料，且 BACPAC 副檔名的 zip 檔案。 這可以使用 hello [Azure 入口網站](https://portal.azure.com/)，hello SQLPackage 命令列公用程式、 SQL Server Management Studio (SSMS) 或 PowerShell。

toolearn 如何 tooexport 資料 tooa BACPAC 檔案，請瀏覽 hello [Azure SQL database tooa BACPAC 檔案匯出](https://docs.microsoft.com/azure/sql-database/sql-database-export)頁面，其中包括上列每個方法的詳細的指示。

如何匯出從 SQL Database 以 hello SQL Server 匯入和匯出精靈 」 的個人資料？

此精靈可協助您將資料從來源 tooa 目的複製。 簡介 toohello 精靈 」 中，包括如何 tooget、 權限資訊，以及如何 tooget 協助 hello 工具，請瀏覽 hello[匯入和匯出資料以 hello SQL Server 匯入和匯出精靈](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)網頁。

如需 hello 精靈步驟的概觀，請瀏覽 hello [hello SQL Server 匯入和匯出精靈 」 中的步驟](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard)網頁。

## <a name="next-steps"></a>後續步驟：

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

