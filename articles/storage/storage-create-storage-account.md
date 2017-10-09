---
title: "aaaHow toocreate 管理或刪除儲存體帳戶中 hello Azure 入口網站 |Microsoft 文件"
description: "建立新的儲存體帳戶、 管理您的帳戶存取金鑰，或刪除 hello Azure 入口網站的儲存體帳戶。 了解標準和進階儲存體帳戶。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: c11c6509e192170db4812f47c389fc1009b94daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>關於 Azure 儲存體帳戶
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>概觀
Azure 儲存體帳戶提供唯一的命名空間 toostore，並存取您的 Azure 儲存體資料物件。 儲存體帳戶中的所有物件會做為群組共同計費。 根據預設，您的帳戶中的 hello 資料會是可用的唯一 tooyou，hello 帳戶擁有者。

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>儲存體帳戶計費
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

> [!NOTE]
> 當您建立 Azure 虛擬機器時，儲存體帳戶會為您自動建立 hello 部署位置中如果您不在該位置中已經有儲存體帳戶。 如此就不需要 toofollow hello 步驟 toocreate 虛擬機器磁碟的儲存體帳戶。 hello 儲存體帳戶名稱將會根據 hello 虛擬機器名稱。 請參閱 hello [Azure 虛擬機器文件](https://azure.microsoft.com/documentation/services/virtual-machines/)如需詳細資訊。
> 
> 

## <a name="storage-account-endpoints"></a>儲存體帳戶端點
每個儲存在 Azure 儲存體中的物件都有一個唯一 URL 位址。 hello 儲存體帳戶名稱 form hello 該位址的子網域。 hello 組合子網域和網域名稱，這是特定 tooeach 服務，形成*端點*儲存體帳戶。

例如，如果您的儲存體帳戶命名為*mystorageaccount*，則 hello 預設端點，您的儲存體帳戶必須：

* Blob 服務：http://*mystorageaccount*.blob.core.windows.net
* 表格服務：http://*mystorageaccount*.table.core.windows.net
* 佇列服務：http://*mystorageaccount*.queue.core.windows.net
* 檔案服務：http://*mystorageaccount.file.core.windows.net*.file.core.windows.net

> [!NOTE]
> Blob 儲存體帳戶只會顯示 hello Blob 服務端點。
> 
> 

藉由附加 hello 儲存體帳戶 toohello 端點中的 hello 物件的位置建立 hello URL 來存取儲存體帳戶中的物件。 例如，blob 位址可能會有如下格式︰http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*。

您也可以設定自訂網域名稱 toouse 與儲存體帳戶。 對於傳統儲存體帳戶，如需詳細資訊，請參閱 [針對 Blob 儲存體端點設定自訂網域名稱](storage-custom-domain-name.md) 。 資源管理員的儲存體帳戶，這項功能尚未加入 toohello [Azure 入口網站](https://portal.azure.com)棒的是，但您可以使用 PowerShell 設定它。 如需詳細資訊，請參閱 hello[組 AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607146.aspx) cmdlet。  

## <a name="create-a-storage-account"></a>建立儲存體帳戶
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello 中樞功能表中，選取 **新增** -> **儲存體** -> **儲存體帳戶**。
3. 輸入儲存體帳戶的名稱。 請參閱[儲存體帳戶端點](#storage-account-endpoints)如需詳細資訊關於如何 hello 儲存體帳戶名稱將會使用的 tooaddress 您 Azure 儲存體中的物件。
   
   > [!NOTE]
   > 儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。
   > 
   > 儲存體帳戶名稱必須在 Azure 中是獨一無二的。 hello Azure 入口網站會指出是否 hello 您選取的儲存體帳戶名稱已在使用中。
   > 
   > 
4. 指定使用 hello 部署模型 toobe:**資源管理員**或**傳統**。 **資源管理員**hello 建議部署模型。 如需詳細資訊，請參閱 [了解資源管理員部署和傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。
   
   > [!NOTE]
   > Blob 儲存體帳戶只能建立使用 hello Resource Manager 部署模型。
   > 
   > 
5. 選取的儲存體帳戶的 hello 類型：**一般用途**或**Blob 儲存體**。 **一般用途**hello 預設值。
   
    如果**一般用途**已選取，然後指定 hello 效能層：**標準**或**Premium**。 hello 預設值是**標準**。 如需標準和進階儲存體帳戶的詳細資訊，請參閱[簡介 tooMicrosoft Azure 儲存體](storage-introduction.md)和[高階儲存體： Azure 虛擬機器工作負載的高效能儲存體](storage-premium-storage.md)。
   
    如果**Blob 儲存體**已選取，然後指定 hello 存取層：**作用**或**Cool**。 hello 預設值是**作用**。 如需詳細資訊，請參閱 [Azure Blob 儲存體：經常存取及不常存取層](storage-blob-storage-tiers.md) 。
6. 選取 hello hello 儲存體帳戶的複寫選項： **LRS**， **GRS**， **RA-GRS**，或**ZRS**。 hello 預設值是**RA-GRS**。 如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。
7. 選取您想在其中 toocreate hello 新儲存體帳戶的 hello 訂用帳戶。
8. 指定新的資源群組，或選取現有的資源群組。 如需資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。
9. 選取儲存體帳戶的 hello 地理位置。 如需各區域可用服務的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services) 。
10. 按一下**建立**toocreate hello 儲存體帳戶。

## <a name="manage-your-storage-account"></a>管理儲存體帳戶
### <a name="change-your-account-configuration"></a>變更帳戶組態
建立儲存體帳戶之後，您可以修改其組態，例如變更 hello hello 帳戶或變更 hello 存取層的 Blob 儲存體帳戶時所使用的複寫選項。 在 hello [Azure 入口網站](https://portal.azure.com)，tooyour 儲存體帳戶中，尋找並按一下瀏覽**組態**下**設定**tooview 和/或變更 hello 帳戶設定。

> [!NOTE]
> 根據 hello 效能層，您可以選擇建立 hello 儲存體帳戶時，可能無法使用某些複寫選項。
> 
> 

變更 hello replication 選項，將會變更您的定價。 如需詳細資訊，請參閱 [Azure 儲存體價格](https://azure.microsoft.com/pricing/details/storage/) 頁面。

Blob 儲存體帳戶、 變更 hello 存取層可能需支付費用 hello 變更此外 toochanging 價格。 請參閱 hello [Blob 儲存體帳戶-定價和計費](storage-blob-storage-tiers.md#pricing-and-billing)如需詳細資訊。

### <a name="manage-your-storage-access-keys"></a>管理儲存體存取金鑰
當您建立儲存體帳戶時，Azure 會產生兩個 512 位元儲存體存取金鑰，以存取 hello 儲存體帳戶時用於驗證。 藉由提供兩個儲存體存取金鑰，Azure 可讓您使用不中斷 tooyour 儲存體服務或存取 toothat 服務 tooregenerate hello 索引鍵。

> [!NOTE]
> 建議您避免將儲存體存取金鑰透露給其他任何人。 toopermit 存取 toostorage 資源卻不用釋出儲存存取金鑰，您可以使用*共用的存取簽章*。 您定義的間隔及 hello 權限，您所指定，共用的存取簽章提供給您的帳戶中存取 tooa 資源。 如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 。
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>檢視並複製儲存體存取金鑰
在 hello [Azure 入口網站](https://portal.azure.com)，瀏覽 tooyour 儲存體帳戶，按一下 **所有設定**，然後按一下**存取金鑰**tooview、 複製和重新產生您的帳戶存取金鑰。 hello**便捷鍵**刀鋒視窗中也包含使用您的主要和次要金鑰，您可以在應用程式中複製 toouse 預先設定的連接字串。

#### <a name="regenerate-storage-access-keys"></a>重新產生儲存體存取金鑰
我們建議您變更 hello tooyour 儲存體帳戶定期 toohelp 保護您的儲存體連接的存取金鑰。 如此您就可以維護連接 toohello 儲存體帳戶使用一個存取金鑰，當您重新產生 hello 其他存取金鑰，則會指派兩個存取金鑰。

> [!WARNING]
> 重新產生存取金鑰，可能會影響 Azure 為您的應用程式相依於 hello 儲存體帳戶中的服務。 使用 hello 存取金鑰 tooaccess hello 儲存體帳戶的所有用戶端必須更新的 toouse hello 新的金鑰。
> 
> 

**媒體服務**-如果您有依存於儲存體帳戶的媒體服務時，您必須重新同步處理 hello 存取金鑰與媒體服務重新產生 hello 索引鍵。

**應用程式**-如果您有 web 應用程式或雲端服務該使用 hello 儲存體帳戶，您將會遺失 hello 連線如果您重新產生金鑰，除非您復原您的金鑰。

**儲存體總管**-如果您使用任何[儲存體總管 中應用程式](storage-explorers.md)，您可能需要 tooupdate hello 儲存體金鑰，而這些應用程式使用。

以下是 hello 輪替儲存體存取金鑰的程序：

1. 更新您的應用程式程式碼 tooreference hello 次要存取金鑰的 hello 儲存體帳戶中的 hello 連接字串。
2. 重新產生儲存體帳戶的 hello 主要存取金鑰。 在 hello**便捷鍵**刀鋒視窗中，按一下**重新產生 Key1**，然後按一下**是**tooconfirm 想 toogenerate 新的金鑰。
3. 更新 hello 連接字串中的程式碼 tooreference hello 新主要存取金鑰。
4. Hello 重新產生次要存取金鑰 hello 中相同的方式。

## <a name="delete-a-storage-account"></a>刪除儲存體帳戶
tooremove 儲存體帳戶，您無法再使用，瀏覽 toohello 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)，然後按一下**刪除**。 刪除儲存體帳戶刪除 hello 整個帳戶，其中包括 hello 帳戶中的所有資料。

> [!WARNING]
> 它是不可能 toorestore 刪除儲存體帳戶，或擷取的任何它所包含刪除之前 hello 內容。 刪除 hello 帳戶之前，您有想 toosave 來確定 tooback 任何項目。 這也會保存 true 的任何資源 hello 帳戶中，一旦刪除 blob、 資料表、 佇列或檔案時，將會永久刪除。
> 
> 

toodelete 與 Azure 虛擬機器相關聯的儲存體帳戶，您必須先確定任何虛擬機器磁碟已被刪除。 如果未先刪除虛擬機器磁碟，然後當您嘗試 toodelete 儲存體帳戶，您會看到類似的錯誤訊息：

    Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.

如果 hello 儲存體帳戶使用 hello 傳統部署模型，您可以依照下列步驟在 hello 移除 hello 虛擬機器磁碟[Azure 入口網站](https://manage.windowsazure.com):

1. 瀏覽 toohello[傳統 Azure 入口網站](https://manage.windowsazure.com)。
2. 瀏覽 toohello 虛擬機器 索引標籤。
3. 按一下 hello 磁碟 索引標籤。
4. 選取資料磁碟，然後按一下 [刪除磁碟]。
5. toodelete 磁碟映像中，瀏覽 toohello 映像 索引標籤，然後刪除 hello 帳戶中儲存的任何影像。

如需詳細資訊，請參閱 hello [Azure 虛擬機器文件](http://azure.microsoft.com/documentation/services/virtual-machines/)。

## <a name="next-steps"></a>後續步驟
* [Microsoft Azure 儲存體總管](../vs-azure-tools-storage-manage-with-storage-explorer.md)是免費的獨立應用程式，可讓您以視覺化方式與在 Windows、 macOS 和 Linux 上的 Azure 儲存體資料 toowork microsoft。
* [Azure Blob 儲存體：經常存取及不常存取層](storage-blob-storage-tiers.md)
* [Azure 儲存體複寫](storage-redundancy.md)
* [設定 Azure 儲存體連接字串](storage-configure-connection-string.md)
* [使用 AzCopy 命令列公用程式的 hello 傳輸資料](storage-use-azcopy.md)
* 請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。

