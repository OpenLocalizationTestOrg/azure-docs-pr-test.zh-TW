---
title: "aaaAzure 待用資料的儲存體服務加密 |Microsoft 文件"
description: "Hello Azure 儲存體服務加密功能 tooencrypt 您的 Azure Blob 儲存體上使用 hello 服務端儲存 hello 資料時，擷取 hello 資料時將其解密。"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: edabe3ee-688b-41e0-b34f-613ac9c3fdfd
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: robinsh
ms.openlocfilehash: 4e03c5704071281a798936d41d86456afcfdec77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-service-encryption-for-data-at-rest"></a>待用資料的 Azure 儲存體服務加密
Azure 儲存體服務加密 (SSE) 中的靜止資料可協助您保護與防衛資料 toomeet 您組織的安全性和相容性的承諾。 利用此功能，Azure 儲存體，自動將加密您的資料之前 toopersisting toostorage，並解密先前 tooretrieval。 hello 加密、 解密和金鑰管理是完全透明 toousers。

hello 下列各節提供詳細的指引如何 toouse hello 儲存體服務加密功能，以及 hello 支援案例和使用者經驗。

## <a name="overview"></a>概觀
Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。 您可以使用[用戶端加密](../storage-client-side-encryption.md)、HTTPs 或 SMB 3.0，在應用程式和 Azure 之間進行傳輸時保護資料的安全。 儲存體服務加密可提供待用加密，並以完全透明的方式處理加密、解密和金鑰管理。 所有的資料會使用 256 位元加密[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，hello 最強的區塊的其中一個這類編碼器使用。

SSE 的運作方式寫入 tooAzure 存放裝置，並可用於 Azure Blob 儲存體和檔案儲存體加密 hello 資料。 這也適用於下列 hello:

* 標準儲存體：Blob 和檔案儲存體的一般用途帳戶及 Blob 儲存體帳戶
* 進階儲存體 
* 所有備援層級 (LRS、ZRS、GRS、RA-GRS)
* Azure Resource Manager 儲存體帳戶 (但不是傳統帳戶) 
* 所有區域。

toolearn 詳細資訊，請參閱 toohello 常見問題集。

tooenable 或停用儲存體服務加密儲存體帳戶，登入到 hello [Azure 入口網站](https://portal.azure.com)並選取儲存體帳戶。 Hello 設定 刀鋒視窗上尋找 hello Blob 服務 > 一節中這個螢幕擷取畫面所示並按一下 加密。

![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption/image1.png)
<br/>*圖 1：為 Blob 服務啟用 SSE (步驟 1)*

![顯示 [加密] 選項的入口網站螢幕擷取畫面](./media/storage-service-encryption/image3.png)
<br/>*圖 2：為檔案服務啟用 SSE (步驟 1)*

按一下 hello 加密設定之後，您可以啟用或停用儲存體服務加密。

![顯示 [加密] 屬性的入口網站螢幕擷取畫面](./media/storage-service-encryption/image2.png)
<br/>*圖 3：為 Blob 和檔案服務啟用 SSE (步驟 2)*

## <a name="encryption-scenarios"></a>加密案例
可以在儲存體帳戶層級啟用儲存體服務加密。 啟用之後，客戶將會選擇哪些服務 tooencrypt。 它支援下列客戶案例 hello:

* 加密 Resource Manager 帳戶中的「Blob 儲存體」和「檔案儲存體」。
* 加密的 Blob 和檔案服務在傳統的儲存體帳戶中一次移轉 tooResource 管理員儲存體帳戶。

SSE 具有下列限制的 hello:

* 不支援傳統儲存體帳戶的加密。
* 啟用 hello 加密之後，現有的資料-SSE 只加密新建立的資料。 如果例如建立新的資源管理員儲存體帳戶，但不啟用加密，而且您上傳 blob 或封存的 Vhd toothat 儲存體帳戶，然後再開啟 SSE，除非它們可以重新撰寫或複製不會加密這些 blob。
* Marketplace 支援-啟用從加密的 Vm 建立 hello Marketplace 使用 hello [Azure 入口網站](https://portal.azure.com)，PowerShell 及 Azure CLI。 hello VHD 基底映像將保持未加密狀態。不過，hello VM 已調整大小之後，執行任何寫入將會加密。
* 系統不會將資料表和佇列資料加密。

## <a name="getting-started"></a>開始使用
### <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>步驟 1：[建立新的儲存體帳戶](../storage-create-storage-account.md)。
### <a name="step-2-enable-encryption"></a>步驟 2︰啟用加密。
您可以啟用加密使用 hello [Azure 入口網站](https://portal.azure.com)。

> [!NOTE]
> 如果您想 tooprogrammatically 啟用或停用的儲存體帳戶的儲存體服務加密 hello 時，您可以使用 hello [Azure 儲存體資源提供者 REST API](https://msdn.microsoft.com/library/azure/mt163683.aspx)，hello[儲存體資源提供者用戶端程式庫適用於.NET](https://msdn.microsoft.com/library/azure/mt131037.aspx)， [Azure PowerShell](/powershell/azureps-cmdlets-docs)，或使用 hello [Azure CLI](../storage-azure-cli.md)。
> 
> 

### <a name="step-3-copy-data-toostorage-account"></a>步驟 3： 複製資料 toostorage 帳戶
如果您啟用 SSE hello Blob 服務時，將會加密寫入 toothat 儲存體帳戶的任何 blob。 已經位於該儲存體帳戶的任何 Blob 直到改寫後，才會加密。 您可以從一個儲存體帳戶 tooone 複製 hello 資料，使用 SSE 加密，或甚至啟用 SSE 和 hello blob 複製一個容器 tooanother toosure 先前的資料都會經過加密。 您可以使用任何下列工具 tooaccomplish hello 這。 這是儲存檔案以及 hello 相同的行為。

#### <a name="using-azcopy"></a>使用 AzCopy
AzCopy 是設計來複製資料 tooand 從 Microsoft Azure Blob、 檔案和資料表儲存體使用簡單的命令，以獲得最佳效能的 Windows 命令列公用程式。 您的 blob 或檔案從一個儲存體帳戶 tooanother 具有 SSE 啟用，您可以使用這個 toocopy。 

toolearn 詳細資訊，請瀏覽[hello AzCopy 命令列公用程式使用傳輸資料](storage-use-azcopy.md)。

#### <a name="using-smb"></a>使用 SMB
Azure 檔案儲存體提供使用標準 SMB 通訊協定 hello hello 雲端中的檔案共用。 您可以從內部部署或 Azure 中的用戶端掛接檔案共用。 掛接之後，如 Robocopy 工具可以使用的 toocopy 檔案經由 tooAzure 檔案共用。 如需詳細資訊，請參閱[如何 toomount Azure 檔案共用上 Windows](../files/storage-how-to-use-files-windows.md)和[toomount Azure 檔案在 Linux 上的共用方式](../storage-how-to-use-files-linux.md)。


#### <a name="using-hello-storage-client-libraries"></a>使用 hello 儲存體用戶端程式庫
您可以複製 blob 或檔案資料 tooand 從 blob 儲存體或使用我們一組豐富的儲存體用戶端程式庫，包括.NET、 c + +、 Java、 Android、 Node.js、 PHP、 Python 和 Ruby 的儲存體帳戶之間。

toolearn 詳細資訊，請造訪我們[開始使用適用於.NET 的 Azure Blob 儲存體使用](../blobs/storage-dotnet-how-to-use-blobs.md)。

#### <a name="using-a-storage-explorer"></a>使用儲存體總管
您可以使用儲存體總管 toocreate 儲存體帳戶，請上傳和下載資料、 檢視內容的 blob，並瀏覽目錄。 您可以使用其中一個這些 tooupload blob tooyour 儲存體帳戶並啟用加密。 使用一些儲存體總管中，您也可以複製現有 blob 儲存體 tooa 不同容器 hello 儲存體帳戶中的資料或新的儲存體帳戶具有 SSE 啟用。

toolearn 詳細資訊，請瀏覽[Azure 儲存體總管](../storage-explorers.md)。

### <a name="step-4-query-hello-status-of-hello-encrypted-data"></a>步驟 4: Hello 查詢 hello 狀態加密資料
已部署可讓您有物件 toodetermine tooquery hello 狀態或不加密過的 hello 儲存體用戶端程式庫的更新的版本。 這目前只能供 Blob 儲存體使用。 支援的檔案儲存體位於 hello 藍圖。 

在 hello 同時，您可以呼叫[取得帳戶屬性](https://msdn.microsoft.com/library/azure/mt163553.aspx)hello 儲存體帳戶的 tooverify 已啟用加密或 hello hello Azure 入口網站中的儲存體帳戶屬性的檢視。

## <a name="encryption-and-decryption-workflow"></a>加密和解密工作流程
以下是 hello 加密/解密工作流程的簡短描述：

* hello 客戶上啟用加密 hello 儲存體帳戶。
* Hello 客戶時寫入新的資料 （PUT Blob，將區塊、 PUT Page、 放置檔案等） tooBlob 或檔案的儲存體。使用 256 位元加密每次寫入[AES 加密](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)，hello 最強的區塊的其中一個這類編碼器使用。
* Hello 客戶需要 tooaccess 資料 （取得 Blob 等） 時，資料時，會自動解密後再傳回 toohello 使用者。
* 如果已停用加密，已不再加密新的寫入，直到 hello 使用者來重新撰寫現有加密的資料仍會維持加密。 雖然加密啟用狀態，將寫入 tooBlob 或檔案的儲存體將會加密。 hello 狀態的資料不會變更與 hello 切換 啟用/停用加密 hello 儲存體帳戶的使用者。
* 所有加密金鑰會由 Microsoft 儲存、加密及管理。

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>待用資料的儲存體服務加密的常見問題集
**問：我有現有的傳統儲存體帳戶。可以在其上啟用 SSE 嗎？**

答︰否，只有 Resource Manager 儲存體帳戶支援 SSE。

**問：我要如何在我的傳統儲存體帳戶中加密資料？**

答： 您可以建立新的資源管理員儲存體帳戶，並將複製程式資料，請使用[AzCopy](storage-use-azcopy.md)從現有的傳統儲存體帳戶 tooyour 新建立的資源管理員儲存體帳戶。 

如果您移轉您的傳統儲存體帳戶 tooa 資源管理員儲存體帳戶，這項作業是在瞬間完成，您的帳戶 hello 類型變更，但不會影響現有的資料。 只有在啟用加密之後，才會加密所有新資料。 如需詳細資訊，請參閱[平台支援移轉的 IaaS 資源從傳統 tooResource 管理員](https://azure.microsoft.com/blog/iaas-migration-classic-resource-manager/)。 請注意，只有針對 Blob 和「檔案」服務才支援此功能。

**問：我有現有的 Resource Manager 儲存體帳戶。可以在其上啟用 SSE 嗎？**

答︰是，但只會加密新寫入的資料。 並不會返回及加密已經存在的資料。 這是尚未支援 hello 檔案儲存體預覽。

**問： 我想要 tooencrypt hello 目前資料中現有的資源管理員儲存體帳戶？**

答︰您可以在 Resource Manager 儲存體帳戶中隨時啟用 SSE。 不過，不會加密已經存在的資料。 tooencrypt 現有的資料，您可以將它們複製 tooanother 名稱或另一個容器，然後再移除 hello 未加密版本。

**問︰我正在使用進階儲存體，我是否可以使用 SSE？**

答︰是，SSE 支援標準儲存體和進階儲存體。  Hello 檔案服務不支援進階儲存體。

**問︰如果我建立新的儲存體帳戶，並啟用 SSE，然後使用該儲存體帳戶建立新的 VM，是否表示我的 VM 會加密？**

答： 會。 建立使用 hello 新儲存體帳戶的任何磁碟都將加密，只要在建立之後啟用 SSE。 如果已在使用 Azure Market Place hello VHD 基底映像建立 VM 的 hello 將保持未加密狀態。不過，hello VM 已調整大小之後，執行任何寫入將會加密。

**問︰是否可以使用 Azure PowerShell 和 Azure CLI 建立新的儲存體帳戶並且啟用 SSE？**

答： 會。

**問︰如果已啟用 SSE，Azure 儲存體的成本會多出多少？**

答：沒有任何額外成本。

**問： 誰管理 hello 加密金鑰？**

答： hello 金鑰是由 Microsoft 管理。

**問︰我可以使用自己的加密金鑰嗎？**

答： 我們會努力提供功能以客戶 toobring 他們自己的加密金鑰。

**問： 是否可以撤銷存取 toohello 加密金鑰？**

答： 不是在這個階段中。hello 金鑰完全是由 Microsoft 管理。

**問︰我建立新的儲存體帳戶時是否預設啟用 SSE？**

答： SSE 不會啟用預設值;您可以使用 Azure 入口網站 tooenable hello 它。 您可以也以程式設計方式啟用此功能使用 hello 儲存體資源提供者 REST API。

**問︰這項功能與 Azure 磁碟加密有什麼不同？**

答： 這項功能是使用的 tooencrypt Azure Blob 儲存體中的資料。 hello Azure 磁碟加密是使用的 tooencrypt 中 IaaS Vm 的 OS 和資料磁碟。 如需詳細資訊，請參閱我們的[儲存體安全性指南](../storage-security-guide.md)。

**問： 如果我啟用 SSE，然後在並 hello 磁碟上啟用 Azure 磁碟加密？**

答︰這會順暢地運作。 這兩種方法都會加密您的資料。

**問： 我的儲存體帳戶設定 toobe 無法重複地理複寫。如果啟用 SSE，我的備援複本是否也會加密？**

A: [是]，加密 hello 儲存體帳戶的所有副本，並支援所有的備援選項 – 在本機備援儲存體 (LRS)、 區域備援儲存體 (ZRS)、 地理備援儲存體 (GRS) 和讀取權異地備援儲存體 (RA-GRS) –。

**問︰我無法在我的儲存體帳戶上啟用加密。**

答︰這是 Resource Manager 儲存體帳戶嗎？ 不支援傳統儲存體帳戶。 

**問︰是否只有在特定區域中允許 SSE？**

答： hello SSE 可在所有區域的 Blob 儲存體。 請檢查檔案儲存的 hello 可用性一節。 

**問： 如何連絡有人如果我有任何問題或想 tooprovide 意見反應？**

答： 請連絡[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com)是否有任何問題相關 tooStorage 服務加密。

## <a name="next-steps"></a>後續步驟
Azure 儲存體提供一組完整的安全性功能，同時讓開發人員 toobuild 安全的應用程式。 如需詳細資訊，請瀏覽 hello[存放安全性指南 》](../storage-security-guide.md)。

