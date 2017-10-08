---
title: "資料湖存放區中的存取控制的 aaaOverview |Microsoft 文件"
description: "了解 Azure Data Lake Store 中的存取控制運作方式"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Azure Data Lake Store 中的存取控制

Azure Data Lake Store 實作衍生自 HDFS，又衍生自 hello POSIX 存取控制模型的存取控制模型。 本文摘要說明 hello hello 存取控制模型的資料湖存放區的基本概念。 toolearn 進一步了解 hello HDFS 存取控制模型，請參閱[HDFS 權限指南](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)。

## <a name="access-control-lists-on-files-and-folders"></a>檔案和資料夾的存取控制清單

存取控制清單 (ACL) 有兩種類型，**存取 ACL** 和**預設 ACL**。

* **存取 Acl**： 這些控制項存取 tooan 物件。 檔案和資料夾均有存取 ACL。

* **預設 Acl**: 「 範本 」 的 Acl 判斷 hello 存取 Acl，該資料夾下建立所有子系項目的資料夾與相關聯。 檔案沒有預設 ACL。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

存取 Acl 和預設 Acl 有 hello 相同的結構。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> 父代上的變更 hello 預設 ACL 不會影響 hello 存取 ACL 或預設的子項目已存在的 ACL。
>
>

## <a name="users-and-identities"></a>使用者和身分識別

每個檔案和資料夾都有這些身分識別的不同權限︰

* hello 擁有 hello 檔案的使用者
* hello 擁有的群組
* 具名使用者
* 具名群組
* 所有其他使用者

hello 身分識別的使用者和群組是 Azure Active Directory (Azure AD) 身分識別。 因此除非另有說明 」 中的使用者，"hello 內容的資料湖存放區，可以是表示 Azure AD 使用者或 Azure AD 安全性群組。

## <a name="permissions"></a>權限

hello 物件的權限的檔案系統是**讀取**，**寫入**，和**Execute**，也可以用檔案及資料夾 hello 下表所示：

|            |    檔案     |   資料夾 |
|------------|-------------|----------|
| **讀取 (R)** | 可以讀取檔案的 hello 內容 | 需要**讀取**和**Execute** toolist hello hello 資料夾內容|
| **寫入 (W)** | 可以寫入或附加 tooa 檔案 | 需要**寫入**和**Execute** toocreate 資料夾的子系項目 |
| **執行 (X)** | 並不表示 hello 內容資料湖存放區中的任何項目 | 需要的 tootraverse hello 子資料夾的項目 |

### <a name="short-forms-for-permissions"></a>權限的簡短形式

**RWX**是使用的 tooindicate**讀取 + 寫入 + 執行**。 更緊縮的數字形式存在於其中**讀取 = 4**，**寫入 = 2**，和**Execute = 1**，hello 總和代表 hello 權限。 以下有一些範例。

| 數值形式 | 簡短形式 |      意義     |
|--------------|------------|------------------------|
| 7            | RWX        | 讀取 + 寫入 + 執行 |
| 5            | R-X        | 讀取 + 執行         |
| 4            | R--        | 讀取                   |
| 0            | ---        | 沒有權限         |


### <a name="permissions-do-not-inherit"></a>不會繼承權限

資料湖存放區所使用的 hello POSIX 樣式模型，在權限的項目會儲存 hello 項目本身上。 換句話說，無法繼承項目的權限，從 hello 父項目。

## <a name="common-scenarios-related-toopermissions"></a>常見的案例相關的 toopermissions

以下是一些常見的案例 toohelp 您了解哪些權限需要 tooperform Data Lake Store 帳戶上的特定作業。

### <a name="permissions-needed-tooread-a-file"></a>需要 tooread 檔案權限。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Hello 檔案 toobe 讀取，如 hello 呼叫端需要**讀取**權限。
* 針對所有 hello hello 資料夾結構中包含 hello 檔案的資料夾，hello 呼叫端需要**Execute**權限。

### <a name="permissions-needed-tooappend-tooa-file"></a>需要 tooappend tooa 檔案權限。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Hello 檔案 toobe 附加到，如 hello 呼叫端需要**寫入**權限。
* 針對所有 hello 包含 hello 檔案的資料夾，hello 呼叫端需要**Execute**權限。

### <a name="permissions-needed-toodelete-a-file"></a>需要 toodelete 檔案權限。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Hello 父資料夾，hello 呼叫端需要**寫入 + 執行**權限。
* 針對所有 hello hello 檔案的路徑中的其他資料夾，hello 呼叫端需要**Execute**權限。



> [!NOTE]
> 撰寫 hello 檔案的權限不需要的 toodelete 它只要 hello 先前的兩個條件都成立。
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>需要 tooenumerate 資料夾權限。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Hello 資料夾 tooenumerate，如 hello 呼叫端需要**讀取 + Execute**權限。
* 針對所有 hello 上階資料夾，hello 呼叫端需要**Execute**權限。

## <a name="viewing-permissions-in-hello-azure-portal"></a>在 hello Azure 入口網站中的檢視權限

從 hello**資料總管**刀鋒視窗中的 hello Data Lake Store 帳戶按一下**存取**toosee hello Acl 的檔案或資料夾。 按一下**存取**toosee hello Acl hello**目錄**下 hello 資料夾**mydatastore**帳戶。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

在這個刀鋒視窗中，hello 頂部區段會顯示 hello 具備權限，您的概觀。 （在 hello 螢幕擷取畫面，hello 使用者是 Bob）。接下來，會顯示 hello 存取權限。 在這之後，從 hello**存取**刀鋒視窗中，按一下 **簡單檢視**toosee hello 較簡單的檢視。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

按一下**進階檢視**toosee hello 更進階的檢視，其中會顯示 hello 概念的預設 Acl、 遮罩和超級使用者。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>hello 超級使用者

超級使用者具有 hello 大部分的權限的所有 hello 使用者 hello 資料湖存放區中。 超級使用者：

* 也有 RWX 權限**所有**檔案和資料夾。
* 可以變更任何檔案或資料夾的 「 hello 」 權限。
* 可以變更 hello 擁有使用者或擁有的任何檔案或資料夾的群組。

在 Azure 中，Data Lake Store 帳戶具有數個 Azure 角色，包括︰

* 擁有者
* 參與者
* 讀取者

所有人 hello**擁有者**Data Lake Store 帳戶的角色會自動超級使用者該帳戶。 詳細資訊，請參閱 toolearn[角色型存取控制](../active-directory/role-based-access-control-configure.md)。
如果您想 toocreate 超級使用者權限的自訂角色型存取控制 (RBAC) 角色，它會需要下列權限的 toohave hello:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>hello 擁有使用者

建立 hello 項目 hello 使用者會自動為 hello 擁有 hello 項目的使用者。 擁有使用者可以︰

* 變更 hello 檔案擁有者權限。
* 變更 hello 只要 hello 擁有使用者也是 hello 目標群組的成員擁有的擁有的檔案群組。

> [!NOTE]
> 擁有使用者的 hello*無法*變更 hello 擁有另一個擁有檔案的使用者。 只有超級使用者可以變更 hello 擁有檔案或資料夾的使用者。
>
>

## <a name="hello-owning-group"></a>hello 擁有的群組

Hello POSIX Acl，在每個使用者都與 「 主要群組 」。 例如，使用者"alice"可能屬於 toohello"finance"群組。 Alice 也可能屬於 toomultiple 群組，但有一個群組一律指定做為其主要群組。 在 POSIX，Alice 建立檔案，當 hello 擁有該檔案群組的設定 tooher 主要群組，在此情況下為"finance"。

建立新的檔案系統項目時，資料湖存放區會指派值 toohello 擁有群組。

* **案例 1**: hello 根資料夾"/"。 建立 Data Lake Store 帳戶時，會建立這個資料夾。 在此情況下，擁有 hello 的群組設定建立 hello 帳戶 toohello 使用者。
* **案例 2** （每個其他情況下）： hello 擁有的群組建立新的項目時，會複製從 hello 父資料夾。

可以變更 hello 擁有的群組：
* 任何超級使用者。
* 如果 hello 擁有使用者也是 hello 目標群組的成員擁有的使用者，hello。

## <a name="access-check-algorithm"></a>存取檢查演算法

下列圖例的 hello 代表 hello Data Lake Store 帳戶的存取檢查演算法。

![Data Lake Store ACL 演算法](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>hello 遮罩及 「 有效權限 」

hello**遮罩**是 RWX 值都會使用的 toolimit 存取**具名使用者**，hello**擁有群組**，和**具名群組**時執行 hello 存取檢查演算法。 以下是 hello 的 hello 遮罩的重要概念。

* hello 遮罩會建立 「 有效權限。 」 也就是會修改 hello 權限的存取檢查 hello 次。
* hello 遮罩可以直接編輯 hello 檔案擁有者和任何超級使用者。
* hello 遮罩可以移除權限 toocreate hello 有效權限。 hello 遮罩*無法*新增權限 toohello 有效權限。

讓我們看看一些範例。 在下列範例的 hello，hello 遮罩設定太**RWX**，這表示該 hello 遮罩，不會移除任何權限。 hello hello 具名使用者擁有的群組，和名為群組的有效權限不會改變 hello 存取檢查期間。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

在下列範例的 hello，hello 遮罩設定太**R-X**。 這表示它**關閉 hello 寫入權限**如**具名使用者**，**擁有群組**，和**具名群組**時存取的 hello請檢查。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

如需參考，以下是檔案或資料夾的 hello 遮罩 hello Azure 入口網站中出現的位置。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> 新的 Data Lake Store 帳戶、 hello 存取 ACL 的 hello 遮罩和預設 ACL 的 hello 根資料夾 （"/"） 會預設 tooRWX。
>
>

## <a name="permissions-on-new-files-and-folders"></a>新檔案和資料夾的權限

建立新的檔案或資料夾時在現有的資料夾下，判斷 hello hello 父資料夾上的預設 ACL:

- 子資料夾的預設 ACL 與存取 ACL。
- 子檔案的存取 ACL (檔案沒有預設 ACL)。

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>hello 存取子檔案或資料夾的 ACL

建立子檔案或資料夾時，父代 hello 預設 ACL 複製 hello hello 子檔案或資料夾的存取 ACL。 此外，如果**其他**使用者在 hello 父預設 ACL 有 RWX 權限，就會移除從 hello 子系項目的存取 ACL。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

在大部分情況下，hello 先前的資訊會是所有您需要有關如何判斷子系項目的存取 ACL tooknow。 不過，如果您很熟悉與 POSIX 系統和想 toounderstand 深入了解如何達成這項轉換，請參閱 hello 節[Umask 的角色中建立新的檔案及資料夾的 hello 存取 ACL](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders)本文稍後。


### <a name="a-child-folders-default-acl"></a>子資料夾的預設 ACL

父資料夾下建立子資料夾時，hello 父資料夾的預設 ACL 會透過複製，因為是 toohello 子資料夾的預設 ACL。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>可供了解 Data Lake Store 中 ACL 的進階主題

以下是一些您了解如何判斷 Acl 的 Data Lake Store 檔案或資料夾的進階的主題 toohelp。

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>建立新的檔案及資料夾的 hello 存取 ACL Umask 的角色

在 POSIX 相容的系統中，hello 一般概念是該 umask hello 父資料夾的已使用 tootransform hello 權限 9 位元值**擁有使用者**，**擁有群組**，和**其他**hello 存取新的子檔案或資料夾的 ACL 上。 umask hello 位元會識別哪一個位元 tooturn 關閉 hello 子系項目的存取 ACL 中。 因此，它都會使用 tooselectively 防止 hello 傳播的權限**擁有使用者**，**擁有群組**，和**其他**。

Hello umask 在 HDFS 系統中，通常是由系統管理員所控制的 sitewide 組態選項。 Data Lake Store 會使用無法變更的 **全帳戶 umask** 。 下列表格顯示 hello hello 取消遮罩的資料湖存放區。

| 使用者群組  | 設定 | 對新的子項目的存取 ACL 的影響 |
|------------ |---------|---------------------------------------|
| 擁有使用者 | ---     | 沒有影響                             |
| 擁有群組| ---     | 沒有影響                             |
| 其他       | RWX     | 移除讀取 + 寫入 + 執行         |

hello 下列圖例顯示此 umask 作用中。 hello 效果是 tooremove**讀取 + 寫入 + 執行**如**其他**使用者。 因為 hello umask 未指定的位元**擁有使用者**和**擁有群組**，不會轉換這些權限。

![Data Lake Store ACL](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>hello 自黏便箋的位元

hello 自黏便箋的位元為 POSIX filesystem 更進階的功能。 在 hello 內容中的資料湖存放區，不太需要該 hello 自黏便箋的位元。

hello 下表顯示 hello 自黏便箋的位元資料湖存放區中的運作方式。

| 使用者群組         | 檔案    | 資料夾 |
|--------------------|---------|-------------------------|
| 黏性位元 **OFF** | 沒有影響   | 沒有影響。           |
| 黏性位元 **ON**  | 沒有影響   | 防止以外的任何人**超級使用者**和 hello**擁有使用者**項目的刪除或重新命名該子項目。               |

hello 自黏便箋的位元不會顯示 hello Azure 入口網站中。

## <a name="common-questions-about-acls-in-data-lake-store"></a>Data Lake Store 中 ACL 的相關常見問題

以下是有關 Data Lake Store 中 ACL 的一些常見問題。

### <a name="do-i-have-tooenable-support-for-acls"></a>是否有 Acl tooenable 支援？

否。 Data Lake Store 帳戶一律會啟用透過 ACL 的存取控制。

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>需要的 toorecursively 刪除的資料夾和其內容的權限？

* hello 父資料夾必須要有**寫入 + 執行**權限。
* hello 資料夾 toobe 刪除，而且每個資料夾內，需要**讀取 + 寫入 + 執行**權限。

> [!NOTE]
> 您不需要寫入權限 toodelete 檔案資料夾中。 此外，hello 根資料夾"/"可以**從未**被刪除。
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Hello 的檔案或資料夾的擁有者是誰？

hello 的檔案或資料夾的建立者變成 hello 擁有者。

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>哪些群組是設定為 hello 擁有的檔案或資料夾，在建立群組？

從擁有 hello 父資料夾下的 hello 新檔案或資料夾建立群組的 hello 複製 hello 擁有的群組。

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>我是 hello 擁有檔案的使用者，但沒有需要的 hello RWX 權限。 該怎麼辦？

hello 擁有使用者可以變更 hello 權限的 hello 檔案 toogive 本身所需的任何 RWX 權限。

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>當我查看 Acl hello Azure 入口網站中，我看到使用者名稱，但透過應用程式開發介面，看 Guid，為什麼？

Hello Acl 中的項目會儲存為對應 toousers 在 Azure AD 中的 Guid。 hello Api 傳回 hello Guid 原狀。 hello Azure 入口網站嘗試 toomake Acl 更容易 toouse 所轉譯的 hello Guid 為盡可能的易記名稱。

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>為何有時候會看到 hello Acl 中的 Guid 當我使用 hello Azure 入口網站？

當 hello 使用者不在 Azure AD 中不再存在時，會顯示 GUID。 這通常是因為當 hello 使用者已離開 hello 公司，或已從 Azure AD 中刪除其帳戶。

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Data Lake Store 是否支援 ACL 的繼承？

否。

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Hello 遮罩與 umask 之間的差異為何？

| 遮罩 | umask|
|------|------|
| hello**遮罩**屬性上可用的每個檔案和資料夾。 | hello **umask**是 hello Data Lake Store 帳戶的屬性。 因此會有只有單一 umask hello 資料湖存放區中。    |
| 可以更改 hello 擁有使用者或擁有的檔案或超級使用者的群組上的檔案或資料夾的 hello 遮罩屬性。 | hello umask 屬性無法修改任何使用者，即使超級使用者。 這是不能變更的常數值。|
| hello 遮罩屬性會使用於 hello 存取檢查演算法在執行階段 toodetermine 使用者是否具有 hello 右 tooperform 檔案或資料夾中的作業。 hello 遮罩的 hello 角色時的存取檢查 hello 是 toocreate 「 有效權限 」。 | hello umask 不在所有使用存取檢查期間。 hello umask 為使用的 toodetermine hello 存取 ACL 的新子資料夾的項目。 |
| hello 遮罩是 hello 時間的存取檢查會在套用 toonamed 使用者，具名的群組和擁有使用者的 3 位元 RWX 值。| hello umask 是 9 位元值，適用於擁有擁有 群組中，使用者 toohello 和**其他**新子系。|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>何處可以進一步了解 POSIX 存取控制模型？

* [Linux 上的 POSIX 存取控制清單](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [HDFS 權限指南](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [POSIX 常見問題集](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [Ubuntu 上的 POSIX ACL](https://help.ubuntu.com/community/FilePermissionsACLs)

* [Linux 上使用存取控制清單的 ACL](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a>另請參閱

* [Azure Data Lake Store 概觀](data-lake-store-overview.md)
