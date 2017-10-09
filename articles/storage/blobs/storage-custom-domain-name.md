---
title: "您的 Azure Blob 儲存體端點的自訂網域名稱 aaaConfigure |Microsoft 文件"
description: "使用 Azure 儲存體帳戶中的 hello Azure 入口網站 toomap 您自己的正式名稱 (CNAME) toohello Blob 儲存體端點。"
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: bfee6d28039f389ba2e2ed6b28d43894b6e15469
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>針對 Blob 儲存體端點設定自訂網域名稱

您可以設定自訂網域名稱，以供存取 Azure 儲存體帳戶中的 Blob 資料。 Blob 儲存體是 hello 預設端點`<storage-account-name>.blob.core.windows.net`。 如果您將對應的自訂網域和子網域，像是**www.contoso.com** toohello blob 儲存體帳戶的端點，您的使用者可以存取 blob 儲存體帳戶使用該網域中的資料。

> [!IMPORTANT]
> Azure 儲存體尚未以原生方式支援使用自訂網域的 HTTPS。 您可以在目前[使用透過 HTTPS 使用自訂網域的 hello Azure CDN tooaccess blob](storage-https-custom-domain-cdn.md)。
>

hello 下列表格會顯示幾個範例 Url 位於名為的儲存體帳戶的 blob 資料的**mystorageaccount**。 hello 自訂網域註冊 hello 儲存體帳戶是**www.contoso.com**:

| 資源類型 | 預設 URL | 自訂網域 URL |
| --- | --- | --- |
| 儲存體帳戶 | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| Blob |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| 根容器 | http://mystorageaccount.blob.core.windows.net/myblob 或 http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob 或 http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>直接與中繼網域對應

有兩種方式 toopoint 您的自訂網域 toohello blob 端點，您的儲存體帳戶： 直接對應，以及使用 hello CNAME *asverify*中繼子網域。

### <a name="direct-cname-mapping"></a>直接 CNAME 對應

hello 第一個和最簡單方法是 toocreate toohello blob 端點直接對應您的自訂網域和子網域的正式名稱 (CNAME) 記錄。 CNAME 記錄會對應來源網域 tooa 目的地網域的網域名稱系統 (DNS) 功能。 在此情況下，hello 來源網域是您自己的自訂網域和子網域，例如*www.contoso.com*。 hello 目的地網域則是 Blob 服務端點，例如*mystorageaccount.blob.core.windows.net*。

hello 直接的方法在講述[註冊自訂網域](#register-a-custom-domain)。

### <a name="intermediary-mapping-with-asverify"></a>使用 *asverify* 的中繼對應

hello 第二種方法也會使用 CNAME 記錄，但先採用 Azure tooavoid 停機時間所辨識的特殊子網域： **asverify**。

對應您的自訂網域 tooa blob 端點的 hello 程序可能會導致在短暫的停機時間 hello 網域在它註冊在 hello 時[Azure 入口網站](https://portal.azure.com)。 如果您的自訂網域目前支援的應用程式的服務等級合約 (SLA) 要求零停機時間，則您可以使用 hello Azure *asverify*子網域當做中繼註冊步驟。 此中繼步驟可確保使用者 hello DNS 對應時所能 tooaccess 您的網域。

hello 中繼方法在講述[註冊自訂網域使用 hello *asverify*子網域](#register-a-custom-domain-using-the-asverify-subdomain)。

## <a name="register-a-custom-domain"></a>註冊自訂網域
使用此程序 tooregister 您的自訂網域 hello 網域被暫時無法使用 tooyour 使用者，如有任何疑慮，或您的自訂網域目前未裝載應用程式。

如果您的自訂網域目前支援的應用程式，不能有任何停機時間，請遵循 hello 程序中所述[註冊自訂網域使用 hello *asverify*子網域](#register-a-custom-domain-using-the-asverify-subdomain)。

tooconfigure 自訂網域名稱，您必須在 DNS 中建立新的 CNAME 記錄。 hello CNAME 記錄指定的網域名稱的別名。 在此情況下，則會對應 hello 您的自訂網域 toohello Blob 儲存體端點位址儲存體帳戶。

一般而言，您可在網域註冊機構的網站上管理網域的 DNS 設定。 每個註冊機構有相似但稍微不同的方法指定 CNAME 記錄，但 hello 概念是 hello 相同。 一些基本的網域註冊套件不提供的 DNS 設定，因此您可能需要 tooupgrade 您網域的註冊套件之前，您可以建立 hello CNAME 記錄。

1. 瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。
1. 在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**自訂網域**tooopen hello*自訂網域*刀鋒視窗。
1. 登入 tooyour 網域註冊機構的網站，並移至 toohello 管理 DNS 的頁面。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。
1. 用於管理 Cname 尋找 hello > 一節。 您可能會有 toogo tooan 進階的設定 頁面上，並查看 hello 文字**CNAME**，**別名**，或**子網域**。
1. 建立新的 CNAME 記錄並提供子網域別名，如 **www** 或 **photos**。 然後提供主機名稱，也就是您的 Blob 服務端點，格式為 hello **mystorageaccount.blob.core.windows.net** (其中*mystorageaccount* hello 儲存體帳戶名稱)。 hello 主機名稱 toouse 會出現在項目 #1 的 hello*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。
1. Hello hello 文字方塊中*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)，輸入 hello 您的自訂網域名稱，包括 hello 子網域。 例如，若您的網域為 **contoso.com**，且子網域別名為 **www**，請輸入 **www.contoso.com**。如果您的子網域是**相片**，輸入**photos.contoso.com**。 hello 子網域是*必要*。
1. 選取**儲存**上 hello*自訂網域*刀鋒視窗 tooregister 您的自訂網域。 如果 hello 註冊成功時，您會看到已成功更新儲存體帳戶入口網站的通知。

一旦您新的 CNAME 記錄傳播到透過 DNS，您的使用者可以檢視 blob 資料使用自訂網域，只要有 hello 適當的權限。

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>註冊自訂網域使用 hello *asverify*子網域
使用此程序 tooregister 您的自訂網域如果您的自訂網域目前支援的應用程式所需的 SLA 會有任何停機時間。 藉由建立 CNAME 從`asverify.<subdomain>.<customdomain>`太`asverify.<storageaccount>.blob.core.windows.net`，您可以預先註冊您的 Azure 網域。 然後，您可以建立第二個 CNAME 從`<subdomain>.<customdomain>`太`<storageaccount>.blob.core.windows.net`，此時 tooyour 自訂網域時，流量會導向的 tooyour blob 端點。

hello **asverify**子網域是 Azure 所辨識的特殊子網域。 附加在前面`asverify`tooyour 自己的子網域，您允許 Azure toorecognize 您的自訂網域而無需修改 hello hello 網域的 DNS 記錄。 當您不要修改 hello hello 網域的 DNS 記錄時，就會完全不停機的對應的 toohello blob 端點。

1. 瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。
1. 在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**自訂網域**tooopen hello*自訂網域*刀鋒視窗。
1. 登入 tooyour DNS 提供者的網站，並移至 toohello 管理 DNS 的頁面。 您可能會在 **Domain Name**、**DNS** 或 **Name Server Management** 等區段中發現此頁面。
1. 用於管理 Cname 尋找 hello > 一節。 您可能會有 toogo tooan 進階的設定 頁面上，並查看 hello 文字**CNAME**，**別名**，或**子網域**。
1. 建立新的 CNAME 記錄，並提供包含 hello 的子網域別名*asverify*子網域。 例如 **asverify.www** 或 **asverify.photos**。 然後提供主機名稱，也就是您的 Blob 服務端點，格式為 hello **asverify.mystorageaccount.blob.core.windows.net** (其中**mystorageaccount** hello 儲存體帳戶名稱)。 hello 主機名稱 toouse 會出現在 hello 的項目 #2*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)。
1. Hello hello 文字方塊中*自訂網域*刀鋒視窗中 hello [Azure 入口網站](https://portal.azure.com)，輸入 hello 您的自訂網域名稱，包括 hello 子網域。 不包含 *asverify*。 例如，若您的網域為 **contoso.com**，且子網域別名為 **www**，請輸入 **www.contoso.com**。如果您的子網域是**相片**，輸入**photos.contoso.com**。 hello 子網域是必要項。
1. 選取 hello**使用間接 CNAME 驗證**核取方塊。
1. 選取**儲存**上 hello*自訂網域*刀鋒視窗 tooregister 您的自訂網域。 如果 hello 註冊成功時，您會看到一個入口網站的通知，說明已成功更新儲存體帳戶。 此時，您的自訂網域已經通過 Azure 的驗證，但流量 tooyour 網域尚未路由 tooyour 儲存體帳戶。
1. 傳回 tooyour DNS 提供者的網站，並建立另一個對應的子網域 tooyour Blob 服務端點的 CNAME 記錄。 例如，指定做為 hello 子網域**www**或**相片**(不含 hello *asverify*)，hello 做為主機名稱和**mystorageaccount.blob.core.windows.net** (其中**mystorageaccount** hello 儲存體帳戶名稱)。 有了這個步驟中，您的自訂網域的 hello 註冊已完成。
1. 最後，您可以刪除 hello CNAME 記錄，建立包含 hello **asverify**子網域，因為它是必要只做為中間步驟。

一旦您新的 CNAME 記錄傳播到透過 DNS，您的使用者可以檢視 blob 資料使用自訂網域，只要有 hello 適當的權限。

## <a name="test-your-custom-domain"></a>測試自訂網域

您的自訂網域是的 tooconfirm 確實對應 tooyour Blob 服務端點、 建立 blob 儲存體帳戶內的公用容器中。 接著，如果在 web 瀏覽器中，您可以使用 URI 中遵循格式 tooaccess hello blob 的 hello:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

例如，您可能會使用下列 URI tooaccess hello web 表單的 hello **myforms**容器中 hello **photos.contoso.com**自訂子網域：

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>取消註冊自訂網域

tooderegister 自訂網域，您的 Blob 儲存體端點，以使用其中一個 hello 下列程序。

### <a name="azure-portal"></a>Azure 入口網站

Hello Azure 入口網站 tooremove hello 自訂網域 設定中，執行下列 hello:

1. 瀏覽 tooyour 儲存體帳戶中 hello [Azure 入口網站](https://portal.azure.com)。
1. 在下**BLOB 服務**hello 功能表 刀鋒視窗中，選取**自訂網域**tooopen hello*自訂網域*刀鋒視窗。
1. 清除 hello hello 包含您的自訂網域名稱 文字方塊中的內容。
1. 選取 hello**儲存** 按鈕。

當已經成功移除 hello 自訂網域時，您會看到一個入口網站的通知，說明已成功更新儲存體帳戶。

### <a name="azure-cli-20"></a>Azure CLI 2.0

使用 hello [az 儲存體帳戶更新](https://docs.microsoft.com/cli/azure/storage/account#update)CLI 命令，並指定空字串 (`""`) hello`--custom-domain`引數的值 tooremove 自訂網域註冊。

* 命令格式︰

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* 命令範例︰

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

使用 hello[組 AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) PowerShell cmdlet 並指定空字串 (`""`) hello`-CustomDomainName`引數的值 tooremove 自訂網域註冊。

* 命令格式︰

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* 命令範例︰

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>後續步驟
* [對應的自訂網域 tooan Azure 內容傳遞網路 (CDN) 端點](../../cdn/cdn-map-content-to-custom-domain.md)
* [使用自訂網域中的 hello Azure CDN tooaccess blob，透過 HTTPS](storage-https-custom-domain-cdn.md)
