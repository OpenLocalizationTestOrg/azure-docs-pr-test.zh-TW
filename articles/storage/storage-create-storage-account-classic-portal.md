---
title: "aaaHow toocreate 管理或刪除儲存體帳戶中 hello Azure 傳統入口網站 |Microsoft 文件"
description: "建立新的儲存體帳戶、 管理您的帳戶存取金鑰，或刪除 hello Azure 入口網站的儲存體帳戶。 了解標準和進階儲存體帳戶。"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>關於 Azure 儲存體帳戶
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>概觀
Azure 儲存體帳戶可讓您存取 Azure 儲存體中的 toohello Azure Blob、 佇列、 表格和檔案服務。 儲存體帳戶會提供您 Azure 儲存體的資料物件中的 hello 唯一的命名空間。 根據預設，您的帳戶中的 hello 資料會是可用的唯一 tooyou，hello 帳戶擁有者。

儲存體帳戶分為兩種類型：

* 標準儲存體帳戶包含 Blob、資料表、佇列和檔案儲存體。
* 進階儲存體帳戶目前僅支援 Azure 虛擬機器磁碟。 如需進階儲存體的深入概觀，請參閱 [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](storage-premium-storage.md) 。

## <a name="storage-account-billing"></a>儲存體帳戶計費
我們會根據您的儲存體帳戶對 Azure 儲存體使用量計費。 儲存體成本以四項因素為基礎：儲存體容量、複寫配置、儲存體交易和資料輸出。

* 儲存容量是指 toohow 多您的儲存體帳戶分配的您要使用 toostore 資料。 只儲存資料的 hello 成本決定多少資料由您正在儲存，而且複寫的方式。
* 複寫會決定您的資料同時維護了多少複本，以及在哪些位置。
* 交易參考 tooall 讀取和寫入作業 tooAzure 儲存體。
* 資料輸出是指 toodata 流出 Azure 地區。 存取儲存體帳戶中的 hello 資料時應用程式沒有在執行中的 hello 相同的區域是否，應用程式是一項雲端服務或其他類型的應用程式，則您需要付費做為資料出口。 (若為 Azure 服務，您可以採取步驟 toogroup 您的資料和服務在 hello 相同的資料中心 tooreduce 或排除資料輸出費用。)  

hello [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage)頁面提供的儲存容量、 複寫和異動的詳細定價資訊。 hello[資料傳輸定價詳細資料](https://azure.microsoft.com/pricing/details/data-transfers/)頁面會提供做為資料出口詳細定價資訊。

如需儲存體帳戶容量和效能目標的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。

> [!NOTE]
> 當您建立 Azure 虛擬機器時，儲存體帳戶會為您自動建立 hello 部署位置中如果您不在該位置中已經有儲存體帳戶。 如此就不需要 toofollow hello 步驟 toocreate 虛擬機器磁碟的儲存體帳戶。 hello 儲存體帳戶名稱將會根據 hello 虛擬機器名稱。 請參閱 hello [Azure 虛擬機器文件](https://azure.microsoft.com/documentation/services/virtual-machines/)如需詳細資訊。
> 
> 

## <a name="create-a-storage-account"></a>建立儲存體帳戶
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 按一下**新增**hello 在 hello hello 頁面底部的工作列中。 選擇 資料服務 | 儲存體，然後按一下快速建立。
   
    ![NewStorageAccount](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. 在 [URL] 中，輸入儲存體帳戶的名稱。
   
   > [!NOTE]
   > 儲存體帳戶名稱必須介於 3 到 24 個字元的長度，而且只能包含數字和小寫字母。
   > 
   > 儲存體帳戶名稱必須在 Azure 中是獨一無二的。 hello Azure 傳統入口網站會指出是否 hello 您選取的儲存體帳戶名稱已被使用。
   > 
   > 
   
    請參閱[儲存體帳戶端點](#storage-account-endpoints)下方的相關詳細資料如何 hello 儲存體帳戶名稱將會使用的 tooaddress 您 Azure 儲存體中的物件。
4. 在**位置/同質群組**，選取是關閉的 tooyou 或 tooyour 客戶儲存體帳戶的位置。 如果將存取儲存體帳戶中的資料，從另一個 Azure 服務的詳細資訊，例如 Azure 虛擬機器或雲端服務，您可能想 tooselect 同質群組從 hello 清單 toogroup hello 您儲存體帳戶相同的資料中心與其他 Azure 服務您使用 tooimprove 效能和降低成本。
   
    請注意，您必須在儲存體帳戶建立時選取同質群組。 您無法移動現有的帳戶 tooan 同質群組。 如需同質群組的詳細資訊，請參閱下方的 [使用同質群組讓服務位於相同位置](#service-co-location-with-an-affinity-group) 。
   
   > [!IMPORTANT]
   > toodetermine 哪些位置可供您訂用帳戶，您可以呼叫 hello[列出所有資源提供者](https://msdn.microsoft.com/library/azure/dn790524.aspx)作業。 toolist 提供者的 PowerShell，呼叫[Get AzureLocation](https://msdn.microsoft.com/library/azure/dn757693.aspx)。 從.NET 中，使用 hello[清單](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx)hello ProviderOperationsExtensions 類別的方法。
   > 
   > 此外，如需各區域可用服務的詳細資訊，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services) 。
   > 
   > 
5. 如果您有多個 Azure 訂用帳戶，然後 hello**訂用帳戶**欄位會顯示。 在**訂用帳戶**，輸入 hello 想 toouse hello 儲存體帳戶的 Azure 訂用帳戶。
6. 在**複寫**，選取 hello 的儲存體帳戶複寫所需的層級。 複寫選項是地理備援複寫，為您的資料提供最大的持久性建議 hello。 如需 Azure 儲存體複寫選項的詳細資訊，請參閱 [Azure 儲存體複寫](storage-redundancy.md)。
7. 按一下 [ **建立儲存體帳戶**]。
   
    它可能需要幾分鐘的時間 toocreate 儲存體帳戶。 toocheck hello 狀態，您可以監視 hello 在 hello hello Azure 傳統入口網站底部的通知。 建立 hello 儲存體帳戶之後，新的儲存體帳戶有**線上**狀態和可供使用。

![StoragePage](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>儲存體帳戶端點
每個儲存在 Azure 儲存體中的物件都有一個唯一 URL 位址。 hello 儲存體帳戶名稱 form hello 該位址的子網域。 hello 組合子網域和網域名稱，這是特定 tooeach 服務，形成*端點*儲存體帳戶。

例如，如果您的儲存體帳戶命名為*mystorageaccount*，則 hello 預設端點，您的儲存體帳戶必須：

* Blob 服務：http://*mystorageaccount*.blob.core.windows.net
* 表格服務：http://*mystorageaccount*.table.core.windows.net
* 佇列服務：http://*mystorageaccount*.queue.core.windows.net
* 檔案服務：http://*mystorageaccount.file.core.windows.net*.file.core.windows.net

您可以查看 hello 的 hello 存放裝置儀表板上的儲存體帳戶 hello 端點[Azure 傳統入口網站](https://manage.windowsazure.com)一旦建立 hello 帳戶。

藉由附加 hello 儲存體帳戶 toohello 端點中的 hello 物件的位置建立 hello URL 來存取儲存體帳戶中的物件。 例如，blob 位址可能會有如下格式︰http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*。

您也可以設定自訂網域名稱 toouse 與儲存體帳戶。 如需詳細資訊，請參閱 [針對 Blob 儲存體端點設定自訂網域名稱](storage-custom-domain-name.md) 。

### <a name="service-co-location-with-an-affinity-group"></a>使用同質群組讓服務位於相同位置
「同質群組」  是將您的 Azure 服務和 VM 與 Azure 儲存體帳戶依地理位置而形成的群組。 同質群組可以在相同的資料中心或接近 hello 目標使用者對象的 hello 找出電腦工作負載，藉以改善服務效能。 此外，計費費用時所造成的輸出從屬於 hello 的另一個服務存取儲存體帳戶中的資料相同的同質群組。

> [!NOTE]
> toocreate 同質群組，開啟 hello<b>設定</b>區域 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 [<b>同質群組</b>，然後按一下<b>新增同質群組</b>或 hello<b>新增</b>] 按鈕。 您也可以建立和管理同質群組使用 hello Azure 服務管理 API。 如需詳細資訊，請參閱<a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">同質群組的相關作業</a>。
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>檢視、複製和重新產生儲存體存取金鑰
當您建立儲存體帳戶時，Azure 會產生兩個 512 位元儲存體存取金鑰，以存取 hello 儲存體帳戶時用於驗證。 藉由提供兩個儲存體存取金鑰，Azure 可讓您使用不中斷 tooyour 儲存體服務或存取 toothat 服務 tooregenerate hello 索引鍵。

> [!NOTE]
> 建議您避免將儲存體存取金鑰透露給其他任何人。 toopermit 存取 toostorage 資源卻不用釋出儲存存取金鑰，您可以使用*共用的存取簽章*。 您定義的間隔及 hello 權限，您所指定，共用的存取簽章提供給您的帳戶中存取 tooa 資源。 如需詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md) 。
> 
> 

在 [hello [Azure 傳統入口網站](https://manage.windowsazure.com)，使用**管理金鑰**hello 儀表板或 hello**儲存體**tooview、 複製和重新產生 hello 用儲存體存取金鑰] 頁面tooaccess hello Blob、 資料表和佇列服務。

### <a name="copy-a-storage-access-key"></a>複製儲存體存取金鑰
您可以使用**管理金鑰**toocopy 連接字串中的儲存體存取金鑰 toouse。 hello 連接字串需要 hello 儲存體帳戶名稱和驗證金鑰 toouse。 如需有關設定連接資訊字串 tooaccess Azure 儲存體服務，請參閱 <<c0> [ 設定 Azure 儲存體連接字串](storage-configure-connection-string.md)。

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下**儲存體**，然後按一下hello hello 儲存體帳戶 tooopen hello 儀表板名稱。
2. 按一下 [管理金鑰] 。
   
      隨即開啟。
   
    ![Managekeys](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy 儲存體存取金鑰，選取的 hello 文字。 然後按一下滑鼠右鍵並按一下 [複製] 。

### <a name="regenerate-storage-access-keys"></a>重新產生儲存體存取金鑰
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
2. 重新產生儲存體帳戶的 hello 主要存取金鑰。 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)hello 儀表板、 或是 hello**設定**頁面上，按一下**管理金鑰**。 按一下**重新產生**底下 hello 主要存取金鑰，然後按一下**是**tooconfirm 想 toogenerate 新的金鑰。
3. 更新 hello 連接字串中的程式碼 tooreference hello 新主要存取金鑰。
4. 重新產生 hello 次要存取金鑰。

## <a name="delete-a-storage-account"></a>刪除儲存體帳戶
儲存體帳戶，您無法再使用，使用 tooremove**刪除**hello 儀表板或 hello**設定**頁面。 **刪除**刪除 hello 整個儲存體帳戶，包括 hello 帳戶中所有 hello blob、 資料表和佇列。

> [!WARNING]
> 它是不可能 toorestore 刪除儲存體帳戶，或擷取的任何它所包含刪除之前 hello 內容。 刪除 hello 帳戶之前，您有想 toosave 來確定 tooback 任何項目。 這也會保存 true 的任何資源 hello 帳戶中，一旦刪除 blob、 資料表、 佇列或檔案時，將會永久刪除。
> 
> 如果您的儲存體帳戶包含 Azure 虛擬機器的 VHD 檔案，然後您必須刪除任何的映像和磁碟所使用的 VHD 檔案，才能刪除 hello 儲存體帳戶。 首先，停止 hello 虛擬機器，如果它正在執行，然後再刪除它。 toodelete 磁碟上，瀏覽 toohello**磁碟**索引標籤上，並刪除任何的磁碟。 toodelete 映像中，瀏覽 toohello**映像**索引標籤，然後刪除 hello 帳戶中儲存的任何影像。
> 
> 

1. 在 hello [Azure 傳統入口網站](https://manage.windowsazure.com)，按一下 **儲存體**。
2. 除了 hello 名稱 hello 儲存體帳戶項目中任何位置按一下，然後按一下**刪除**。
   
     -或-
   
    按一下 hello hello 儲存體帳戶 tooopen hello 儀表板名稱，然後再按一下**刪除**。
3. 按一下**是**tooconfirm 想 toodelete hello 儲存體帳戶。

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解 Azure 儲存體，請參閱 hello [Azure 儲存體文件](https://azure.microsoft.com/documentation/services/storage/)。
* 請瀏覽 hello [Azure 儲存體團隊部落格](http://blogs.msdn.com/b/windowsazurestorage/)。
* [使用 AzCopy 命令列公用程式的 hello 傳輸資料](storage-use-azcopy.md)

