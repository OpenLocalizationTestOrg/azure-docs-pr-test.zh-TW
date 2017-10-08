---
title: "aaaAzure 計算選項-雲端服務 |Microsoft 文件"
description: "了解 Azure 計算裝載選項以及其運作方式：App Service、雲端服務和虛擬機器"
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
ms.assetid: ed7ad348-6018-41bb-a27d-523accd90305
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e7f109a54c61cc2f37644d39a61d2d932a374587
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-choose-cloud-services-or-something-else"></a>我該選擇雲端服務還是其他服務？
是為您的 Azure 雲端服務的 hello 選擇？ Azure 對於執行的應用程式提供不同的裝載模型。 每個提供一組不同的服務，因此哪一種您的選擇取決於完全您正在嘗試的項目 toodo。

[!INCLUDE [compute-table](../../includes/compute-options-table.md)]

<a name="tellmecs"></a>

## <a name="tell-me-about-cloud-services"></a>我想了解雲端服務
雲端服務是 [平台即服務 (PaaS)](https://azure.microsoft.com/overview/what-is-paas/) 的一個範例。 像[App Service](../app-service-web/app-service-web-overview.md)，這項技術是設計的 toosupport 可擴充、 可靠以及廉價 toooperate。 就像 App Service 上裝載的 Vm，因此也是雲端服務，不過，您可以更充分掌控 hello Vm。 您可以在雲端服務 VM 上安裝您自己的軟體，並且可從遠端加以操控。

![cs_diagram](./media/cloud-services-choose-me/diagram.png)

更充分的控制也意味著較低的易用性。 除非您需要 hello 其他控制選項，否則這通常會更快速且輕鬆 tooget web 應用程式並執行應用程式服務中的 Web 應用程式中比較 tooCloud 服務。

雲端服務角色分為兩種。 hello 差異 hello 兩個是 hello 虛擬機器上裝載您的角色的方式。

* **Web 角色**  
透過 IIS 自動部署和裝載您的應用程式。

* **背景工作角色**  
不使用 IIS，獨立執行您的應用程式。

例如，簡單的應用程式可能只使用單一 Web 角色提供網站服務。 更複雜的應用程式可能會使用 web 角色 toohandle 連入要求的使用者，然後將這些要求傳遞 tooa 進行處理的背景工作角色上。 (此通訊會使用[服務匯流排](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)或 [Azure 佇列](../storage/common/storage-introduction.md))。

Hello 與上圖所示，所有 hello Vm 在 hello 中執行單一應用程式在相同雲端服務。 透過單一公用 IP 位址，與要求的使用者存取 hello 應用程式會自動載入平衡 hello 應用程式的 Vm 之間。 hello 平台[調整，以及部署](cloud-services-how-to-scale.md)hello Vm 雲端服務中的應用程式的方式可避免硬體故障的單一點中。

即使虛擬機器中執行應用程式，它會是重要 toounderstand 雲端服務提供 PaaS 不 IaaS。 以下是有關它的其中一種方式 toothink： 與 IaaS，例如 Azure 虛擬機器中，您先建立並設定您的應用程式中，執行 hello 環境然後部署至此環境的應用程式。 您負責管理的世界中，許多動作，例如部署的 hello 作業系統每個 VM 中的新修補的版本。 在 PaaS，相反地，就如同 hello 環境已經存在。 您只需要 toodo 是部署您的應用程式。 管理 hello 平台上，執行包含部署新版本的 hello 作業系統中，會為您處理。

## <a name="scaling-and-management"></a>調整和管理
藉由雲端服務，您不需要建立虛擬機器。 不過，您提供的組態檔，會告訴 Azure 多少每個您想要例如**三個 web 角色執行個體**和**兩個背景工作角色執行個體**，和 hello 平台會為您建立它們。  您仍然可以選擇這些支援 VM 的 [大小](cloud-services-sizes-specs.md) ，但您不需自行建立這些 VM。 如果您的應用程式需要 toohandle 更高的負載，您可以要求更多的 Vm，Azure 會建立這些執行個體。 如果 hello 負載降低，您可以關閉這些執行個體，並停止支付它們。

雲端服務應用程式通常會透過兩個步驟的程序的可用 toousers。 開發人員第一個[上傳 hello 應用程式](cloud-services-how-to-create-deploy.md)toohello 平台的臨時區域。 Hello 開發人員就緒時 live toomake hello 應用程式時，它們使用 hello Azure 入口網站 tooswap 預備與生產環境。 這[預備和生產環境之間切換](cloud-services-nodejs-stage-application.md)即可不中斷的情況，它可讓執行中應用程式會升級的 tooa 新版本，而不會影響其使用者。

## <a name="monitoring"></a>監視
雲端服務也提供監視。 像 Azure 虛擬機器中，它會偵測失敗的實體伺服器並重新啟動新電腦上的該伺服器所執行的 hello Vm。 不過，雲端服務也會偵測故障的 VM 和應用程式，而不只是硬體故障。 不同於虛擬機器，它具有每個 web 和背景工作角色內代理程式，因此它無法 toostart 新 Vm 和發生錯誤時的應用程式執行個體。

hello 的雲端服務的 PaaS 本質也有其他的含意。 Hello 最重要的是，在這項技術建置的應用程式應該寫入 toorun 正確任何 web 或背景工作角色執行個體失敗時。 雲端服務應用程式不應該維護這個狀態中的 tooachieve hello 它自己的 Vm 檔案系統。 不同於建立與 Azure 虛擬機器的 Vm，寫入 tooCloud 服務 Vm 不是持續性;沒有類似的虛擬機器資料磁碟。 相反地，雲端服務應用程式應該明確地撰寫所有狀態 tooSQL 資料庫中，blob，資料表或其他外部存放裝置。 如此一來建置應用程式可讓它們更容易 tooscale 和更能抵抗 toofailure，這兩個重要的目標雲端服務。

## <a name="next-steps"></a>後續步驟
[在 .NET 中建立雲端服務應用程式](cloud-services-dotnet-get-started.md)  
[在 Node.js 中建立雲端服務應用程式](cloud-services-nodejs-develop-deploy-app.md)  
[在 PHP 中建立雲端服務應用程式](../cloud-services-php-create-web-role.md)  
[在 Python 中建立雲端服務應用程式](cloud-services-python-ptvs.md)

