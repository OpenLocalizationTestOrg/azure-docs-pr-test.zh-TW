---
title: "Azure 和 Azure 堆疊，當您使用服務，並建置應用程式的 aaaKey 差異 |Microsoft 文件"
description: "配備 tooknow 當您使用服務或 Azure 堆疊建置應用程式。"
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: c81f551d-c13e-47d9-a5c2-eb1ea4806228
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: twooley
ms.openlocfilehash: e302f20aeb3c74f944cb3daaee7e0db073ab5bfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="key-considerations-using-services-or-building-apps-for-azure-stack"></a>關鍵考量：使用服務或為 Azure Stack 建置應用程式

使用服務或為 Azure Stack 建置應用程式時，您必須了解 Azure Stack 與 Azure 之間有所差異。 混合式雲端開發環境做為目標 Azure 堆疊時，本文將提供概觀 hello 重要考量。

## <a name="overview"></a>概觀

Azure Stack 是混合式雲端平台，可讓您從您的公司或服務提供者的資料中心使用 Azure 服務。 身為開發人員，您可以建置在 Azure Stack 上執行的應用程式。 然後，您可以部署這些應用程式 tooAzure 堆疊，tooAzure，或您真的可以建置利用 hello Azure 堆疊雲端與 Azure 之間的連線的混合式應用程式。

您的 Azure 堆疊的雲端系統管理員或服務提供者可讓您知道哪些服務可供您 toouse tooget 如何支援。 他們會透過其自訂方案和供應項目來提供這些服務。

hello Azure 技術的內容會假設應用程式，正在開發 Azure 服務，而不是 Azure 堆疊。 當您建置和部署應用程式 tooAzure 堆疊時，必須了解的一些主要差異，例如：

* Azure 堆疊傳遞 hello 服務和 Azure 中提供的功能的子集。
* 您的公司或服務提供者可以選擇哪些服務希望 toooffer。 這包括自訂的服務或應用程式。
* 您必須使用 hello 修正 Azure 堆疊特定端點 （例如 hello hello 入口網站的位址和 hello Azure 資源管理員端點的 Url）。
* 您必須使用 Azure Stack 所支援的 PowerShell 和 API 版本。 這樣可確保您的應用程式可同時在 Azure Stack 和 Azure 中運作。

## <a name="cheat-sheet-high-level-differences"></a>功能提要：高層差異

hello 下表描述 hello 高階 Azure 堆疊與 Azure 之間的差異。 當您為 Azure Stack 進行開發，或使用 Azure Stack 服務時，請記住這些事項。

| 領域 | Azure (全域) | Azure Stack |
| -------- | ------------- | ----------|
| 由誰操作？ | Microsoft | 您的公司或服務提供者。|
| 尋求支援的連絡對象？ | Microsoft | 如需 Azure 堆疊開發套件支援，請瀏覽 hello [Microsoft 論壇](https://social.msdn.microsoft.com/Forums/home?forum=azurestack)。 Hello 開發套件是評估環境，因為沒有提供透過 Microsoft 客戶支援服務 (CSS) 提供官方支援。
| 可用服務 | 請參閱 hello 清單[Azure 產品](https://azure.microsoft.com/services/?b=17.04b)。 可用的服務因 Azure 區域而異。 | Azure Stack 支援 Azure 服務的子集。 <br><br>實際的服務會根據您的公司或服務提供者選擇 toooffer 而異。
| Azure Resource Manager 端點* | https://management.azure.com | Hello 開發套件： https://management.local.azurestack.external
| 入口網站 URL* | [https://portal.azure.com](https://portal.azure.com) | Hello 開發套件： https://portal.local.azurestack.external
| 區域 | 您可以選取您想要的 toodeploy 至哪個區域。 | Hello 開發套件，一律為區域**本機**。 <br><br>hello 開發套件支援只有一個區域。
| 資源群組 | 資源群組可以跨區域。 | Hello 開發套件，會有只有一個區域。
|支援的命名空間、資源類型和 API 版本 | 最新 hello （或更早版本，尚不被取代）。 | Azure Stack 支援特定版本。 請參閱這篇文章 hello < 版本需求 > 一節。
| | |

* 如果您是 Azure 堆疊雲端操作員，請參閱[使用 Azure 堆疊中的 hello 系統管理員和使用者入口網站](azure-stack-manage-portals.md)hello 系統管理員入口網站和管理員資源管理員端點 Url 的相關資訊。

## <a name="helpful-tools-and-best-practices"></a>實用工具和最佳作法
 
 Microsoft 提供數個工具和指引來協助您為 Azure Stack 進行開發。

| 建議 | 參考 | 
| -------- | ------------- | 
| 開發人員工作站上安裝 hello 正確工具。 | - [安裝 PowerShell](azure-stack-powershell-install.md)<br>- [下載工具](azure-stack-powershell-download.md)<br>- [設定 PowerShell](azure-stack-powershell-configure-user.md)<br>- [安裝 Visual Studio](azure-stack-install-visual-studio.md) 
| 檢閱有關 hello 下列資訊：<br>- Azure Resource Manager 範本考量<br>-如何 toofind 快速入門範本<br>-使用 Azure toodevelop 用於 Azure 堆疊原則模組 toohelp | [開發 Azure Stack](azure-stack-developer.md) | 
| 檢閱並遵循 hello 的範本的最佳作法。 | [Resource Manager 快速入門範本](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md#best-practices)
| | |

## <a name="version-requirements"></a>版本需求

Azure Stack 支援特定版本的 Azure PowerShell 和 Azure 服務 API。 您必須使用支援的版本 tooensure tooboth Azure 堆疊和 tooAzure，可以部署應用程式。

確定您使用 Azure PowerShell，使用正確版本的 toomake [API 版本設定檔](azure-stack-version-profiles.md)。 toodetermine hello 最新 API 版本設定檔，您可以使用，您必須知道您所使用的 Azure 堆疊的組建。 您可以向您的 Azure Stack 系統管理員取得這項資訊。

>[!NOTE]
 如果您正在使用 hello Azure 堆疊開發套件，且您有系統管理存取權，請參閱 hello"判斷 hello 目前版本 > 一節[管理更新](https://docs.microsoft.com/azure/azure-stack/azure-stack-updates#determine-the-current-version)toodetermine hello Azure 堆疊組建。

對於其他應用程式開發介面，執行下列 PowerShell 命令 toooutput hello 命名空間、 資源類型和您 Azure 堆疊訂用帳戶中支援的 API 版本的 hello。 請注意，可能仍有屬性層級的差異。 (這個命令 toowork，您必須已經[安裝](azure-stack-powershell-install.md)和[設定](azure-stack-powershell-configure-user.md)PowerShell for Azure 堆疊環境。 您也必須擁有的訂用帳戶 tooan Azure 堆疊優惠。）

 ```powershell
Get-AzureRmResourceProvider | Select ProviderNamespace -Expand ResourceTypes | Select * -Expand ApiVersions | `
Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} 
```

範例輸出 (已截斷)：![Get-AzureRmResourceProvider 命令的範例輸出](media/azure-stack-considerations/image1.png)
 
## <a name="next-steps"></a>後續步驟

如需在服務層級差異的詳細資訊，請參閱：

* [Azure Stack 中虛擬機器的考量](azure-stack-vm-considerations.md)
* [Azure Stack 中儲存體的考量](azure-stack-acs-differences.md)
* [Azure Stack 網路服務的注意事項](azure-stack-network-differences.md)

