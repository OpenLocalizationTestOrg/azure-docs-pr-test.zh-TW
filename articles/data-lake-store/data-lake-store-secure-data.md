---
title: "aaaSecuring 資料儲存在 Azure Data Lake Store |Microsoft 文件"
description: "了解如何 toosecure 資料在 Azure 資料湖存放區使用群組和存取控制清單"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ca35e65f-3986-4f1b-bf93-9af6066bb716
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 2b4ed7e322e1843ca47d6968ec8801ac19ea6399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securing-data-stored-in-azure-data-lake-store"></a>保護儲存在 Azure 資料湖儲存區中的資料
保護儲存在 Azure 資料湖儲存區中的資料，其方法有三步驟。

1. 首先，在 Azure Active Directory (AAD) 中建立安全性群組。 使用這些安全性群組在 Azure 入口網站的 tooimplement 角色型存取控制 (RBAC)。 如需詳細資訊，請參閱 [Microsoft Azure 中的角色型存取控制](../active-directory/role-based-access-control-configure.md)。
2. 指派 hello AAD 安全性群組 toohello Azure Data Lake Store 帳戶。 這會控制從 hello 入口網站和管理作業，從 hello 入口網站或應用程式開發介面存取 toohello Data Lake Store 帳戶。
3. 存取控制清單 (Acl) hello Data Lake Store 檔案系統上，將指派 hello AAD 安全性群組。
4. 此外，您也可以設定 IP 位址範圍的用戶端可以存取資料湖存放區中的 hello 資料。

這篇文章提供如何 toouse hello Azure 入口網站 tooperform hello 上述工作的指示。 深入了解如何資料湖存放區實作 hello 帳戶和資料層級安全性的詳細資訊，請參閱[Azure 資料湖存放區中的安全性](data-lake-store-security-overview.md)。 如需 ACL 如何在 Azure Data Lake Store 中實作的深入資訊，請參閱 [Data Lake Store 中的存取控制的概觀](data-lake-store-access-control.md)。

## <a name="prerequisites"></a>必要條件
開始本教學課程之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
* **Azure Data Lake Store 帳戶**。 如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)

## <a name="create-security-groups-in-azure-active-directory"></a>在 Azure Active Directory 中建立安全性群組
如需有關指示 toocreate AAD 安全性群組以及 toohello tooadd users 的群組，請參閱[管理 Azure Active Directory 中的安全性群組](../active-directory/active-directory-accessmanagement-manage-groups.md)。

> [!NOTE] 
> 您可以新增使用者及其他群組 tooa hello Azure 入口網站，使用 Azure AD 中。 不過，在排序 tooadd 服務主體 tooa 群組，請使用[Azure AD PowerShell 模組](../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md)。
> 
> ```powershell
> # Get hello desired group and service principal and identify hello correct object IDs
> Get-AzureADGroup -SearchString "<group name>"
> Get-AzureADServicePrincipal -SearchString "<SPI name>"
> 
> # Add hello service principal toohello group
> Add-AzureADGroupMember -ObjectId <Group object ID> -RefObjectId <SPI object ID>
> ```
 
## <a name="assign-users-or-security-groups-tooazure-data-lake-store-accounts"></a>指派使用者或安全性群組 tooAzure Data Lake Store 帳戶
當您指定使用者或安全性群組 tooAzure Data Lake Store 帳戶時，您可以控制 hello 帳戶使用 hello Azure 入口網站和 Azure 資源管理員 Api 存取 toohello 管理作業。 

1. 開啟 Azure 資料湖儲存區帳戶。 從 hello 左窗格中，按一下 **瀏覽**，按一下  **Data Lake Store**，然後從 hello Data Lake Store 刀鋒視窗中，按一下 hello 帳戶名稱 toowhich 想 tooassign 使用者或安全性群組的群組。

2. 在 Data Lake Store 帳戶設定刀鋒視窗中，按一下 [存取控制 (IAM)]。 hello 刀鋒視窗的預設清單**訂閱管理員**群組作為擁有者。
   
    ![指定安全性群組 tooAzure Data Lake Store 帳戶](./media/data-lake-store-secure-data/adl.select.user.icon.png "指派安全性群組 tooAzure Data Lake Store 帳戶")

    有兩種方式 tooadd 群組並指派相關的角色。
   
    * 新增使用者/群組 toohello 帳戶，然後指派角色，或
    * 加入角色，然後指派使用者/群組 toorole。
     
    在本節中，我們查看 hello 第一種方法，加入群組，然後指派角色。 您可以執行類似的步驟 toofirst 選取角色，並再將群組 toothat 角色指派。
4. 在 hello**使用者**刀鋒視窗中，按一下**新增**tooopen hello**新增存取**刀鋒視窗。 在 hello**新增存取**刀鋒視窗中，按一下**選取角色**，然後選取 hello 使用者/群組的角色。
   
    ![新增 hello 使用者角色](./media/data-lake-store-secure-data/adl.add.user.1.png "新增 hello 使用者角色")
   
    hello**擁有者**和**參與者**角色上 hello 資料湖帳戶提供存取 tooa 多種管理功能。 如果與 hello 資料湖資料互動的使用者，您可以將它們 toohello * * 讀取器 * * 角色。 這些角色 hello 範圍會限制的 toohello 管理作業相關的 toohello Azure Data Lake Store 帳戶。
   
    資料作業個別的檔案系統權限會定義 hello 使用者可以執行的動作。 因此，讓讀取者角色的使用者可以只檢視系統管理設定 hello 帳戶相關聯，但可以可能讀取和寫入資料根據檔案系統權限指派 toothem。 Data Lake Store 檔案系統權限詳述在[指派安全性群組 Acl toohello Azure Data Lake Store 檔案系統為](#filepermissions)。
5. 在 hello**新增存取**刀鋒視窗中，按一下 **將使用者新增**tooopen hello**將使用者新增**刀鋒視窗。 在這個刀鋒視窗中，尋找您稍早在 Azure Active Directory 中建立的 hello 安全性群組。 如果您有大量從群組 toosearch，使用 hello 文字方塊在 hello 頂端 toofilter hello 群組名稱。 按一下 [選取] 。
   
    ![新增安全性群組](./media/data-lake-store-secure-data/adl.add.user.2.png "新增安全性群組")
   
    如果您想 tooadd 未列出群組/使用者，您可以邀請他們使用 hello**邀請**圖示，並指定 hello hello 使用者/群組的電子郵件地址。
6. 按一下 [確定] 。 您應該會看到加入如下所示的 hello 安全性群組。
   
    ![已新增的安全性群組](./media/data-lake-store-secure-data/adl.add.user.3.png "已新增的安全性群組")

7. 您的使用者/安全性群組現在具有存取 toohello Azure Data Lake Store 帳戶。 如果您想 tooprovide 存取 toospecific 使用者時，您可以將其加入 toohello 安全性群組。 同樣地，如果您想要使用者的 toorevoke 存取，您可以從 hello 安全性群組加以移除。 您也可以指派多個安全性群組 tooan 帳戶。 

## <a name="filepermissions"></a>將使用者或安全性群組指派為 Acl toohello Azure Data Lake Store 檔案系統
藉由指定使用者/安全性群組 toohello Azure 資料湖檔案系統，您可以設定儲存於 Azure 資料湖存放區中的 hello 資料的存取控制。

1. 在您的 [資料湖儲存區帳戶] 刀鋒視窗中，按一下 [資料總管] 。
   
    ![在 Data Lake Store 帳戶中建立目錄](./media/data-lake-store-secure-data/adl.start.data.explorer.png "在 Data Lake Store 帳戶中建立目錄")
2. 在 hello**資料總管**刀鋒視窗中，按一下 hello 檔案或資料夾，您想 tooconfigure hello ACL，然後再按一下**存取**。 tooassign ACL tooa 檔案，您必須按一下**存取**從 hello**檔案預覽**刀鋒視窗。
   
    ![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-secure-data/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")
3. hello**存取**刀鋒視窗會列出 hello 標準權限和自訂存取已指派 toohello 根。 按一下 hello**新增**圖示 tooadd 自訂層級的 Acl。
   
    ![列出標準和自訂存取](./media/data-lake-store-secure-data/adl.acl.2.png "列出標準和自訂的存取")
   
   * **標準存取**是 hello UNIX 樣式存取，讓您指定讀取、 寫入、 執行 (rwx) toothree 相異使用者類別： 擁有者、 群組和其他項目。
   * **自訂存取**對應 toohello POSIX Acl 可讓您 tooset 特定的使用者名稱或群組，並不只 hello 檔案的擁有者或群組權限。 
     
     如需詳細資訊，請參閱 [HDFS ACLs](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists)。 如需 ACL 如何在 Data Lake Store 中實作的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。
4. 按一下 hello**新增**圖示 tooopen hello**加入自訂存取**刀鋒視窗。 在這個刀鋒視窗中，按一下**選取使用者或群組**，然後在**選取使用者或群組**刀鋒視窗中，尋找您稍早在 Azure Active Directory 中建立的 hello 安全性群組。 如果您有大量從群組 toosearch，使用 hello 文字方塊在 hello 頂端 toofilter hello 群組名稱。 按一下您想 tooadd，然後按一下 hello 群組**選取**。
   
    ![加入群組](./media/data-lake-store-secure-data/adl.acl.3.png "加入群組")
5. 按一下**選取權限**選取 hello 權限，是否要為一份預設 ACL 將 tooassign hello 權限，存取 ACL，或兩者。 按一下 [確定] 。
   
    ![指派權限 toogroup](./media/data-lake-store-secure-data/adl.acl.4.png "指派權限 toogroup")
   
    如需有關 Data Lake Store 中的權限及預設/存取 ACL 的詳細資訊，請參閱 [Data Lake Store 中的存取控制](data-lake-store-access-control.md)。
6. 在 hello**加入自訂存取**刀鋒視窗中，按一下**確定**。 hello 新加入的群組相關聯的 hello 權限，現在會列在 hello**存取**刀鋒視窗。
   
    ![指派權限 toogroup](./media/data-lake-store-secure-data/adl.acl.5.png "指派權限 toogroup")
   
   > [!IMPORTANT]
   > 在 hello 目前版本中，您可以只有 9 的項目底下**自訂存取**。 如果您希望 tooadd 9 個以上的使用者，您應該建立安全性群組，將使用者 toosecurity 群組，將提供的存取權 toothose 安全性群組 hello Data Lake Store 帳戶。
   > 
   > 
7. 如有需要，您也可以在新增 hello 群組之後修改 hello 存取權限。 清除或選取 hello 核取方塊，每個權限類型 （讀取、 寫入、 執行） 根據您是否要 tooremove，或指派該權限 toohello 安全性群組。 按一下**儲存**toosave hello 變更，或**捨棄**tooundo hello 變更。

## <a name="set-ip-address-range-for-data-access"></a>設定資料存取的 IP 位址範圍
Azure Data Lake Store 可讓您存取在網路層級 tooyour 資料存放區的 toofurther 鎖定。 您可以啟用防火牆、指定 IP 位址或為受信任的用戶端定義 IP 位址範圍。 啟用之後，只有擁有 hello 定義之範圍內的 IP 位址的用戶端可以連接到 toohello 存放區。

![防火牆設定和 IP 存取](./media/data-lake-store-secure-data/firewall-ip-access.png "防火牆設定和 IP 位址")

## <a name="remove-security-groups-for-an-azure-data-lake-store-account"></a>移除 Azure 資料湖儲存區帳戶的安全性群組
當您從 Azure Data Lake Store 帳戶移除安全性群組時，您只變更 hello 帳戶使用 hello Azure 入口網站和 Azure 資源管理員 Api 存取 toohello 管理作業。

1. 在您的 [Data Lake Store 帳戶] 刀鋒視窗中，按一下 [設定]。 從 hello**設定**刀鋒視窗中，按一下 **使用者**。
   
    ![指定安全性群組 tooAzure 資料湖帳戶](./media/data-lake-store-secure-data/adl.select.user.icon.png "指派安全性群組 tooAzure 資料湖帳戶")
2. 在 hello**使用者**刀鋒視窗中按一下您想要 tooremove hello 安全性群組。
   
    ![安全性群組 tooremove](./media/data-lake-store-secure-data/adl.add.user.3.png "安全性群組 tooremove")
3. 在 hello 刀鋒視窗中的 hello 安全性群組，按一下 **移除**。
   
    ![已移除的安全性群組](./media/data-lake-store-secure-data/adl.remove.group.png "已移除的安全性群組")

## <a name="remove-security-group-acls-from-azure-data-lake-store-file-system"></a>從 Azure 資料湖儲存區檔案系統移除安全性群組 ACL
當您從 Azure Data Lake Store 檔案系統中移除 Acl 的安全性群組時，您可以變更存取 toohello hello 資料湖存放區中的資料。

1. 在您的 [資料湖儲存區帳戶] 刀鋒視窗中，按一下 [資料總管] 。
   
    ![在 Data Lake 帳戶中建立目錄](./media/data-lake-store-secure-data/adl.start.data.explorer.png "在 Data Lake 帳戶中建立目錄")
2. 在 [hello**資料總管**刀鋒視窗中，按一下 hello 檔案或資料夾，您會想 tooremove hello ACL，並在您的帳戶] 刀鋒視窗中，按一下 hello**存取**圖示。 tooremove ACL 的檔案，您必須按一下**存取**從 hello**檔案預覽**刀鋒視窗。
   
    ![設定 Data Lake 檔案系統上的 ACL](./media/data-lake-store-secure-data/adl.acl.1.png "設定 Data Lake 檔案系統上的 ACL")
3. 在 hello**存取**刀鋒視窗中的，從 hello**自訂存取**區段中，按一下您想要 tooremove hello 安全性群組。 在 hello**自訂存取**刀鋒視窗中，按一下 **移除**，然後按一下**確定**。
   
    ![指派權限 toogroup](./media/data-lake-store-secure-data/adl.remove.acl.png "指派權限 toogroup")

## <a name="see-also"></a>另請參閱
* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
* [從 Azure 儲存體 Blob tooData 湖存放區複製資料](data-lake-store-copy-data-azure-storage-blob.md)
* [搭配 Data Lake Store 使用 Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [搭配資料湖存放區使用 Azure HDInsight](data-lake-store-hdinsight-hadoop-use-portal.md)
* [使用 PowerShell 開始使用資料湖存放區](data-lake-store-get-started-powershell.md)
* [使用 .NET SDK 開始使用資料湖存放區](data-lake-store-get-started-net-sdk.md)
* [存取 Data Lake Store 的診斷記錄](data-lake-store-diagnostic-logs.md)

