---
title: "Service Fabric 和容器 aaaOverview |Microsoft 文件"
description: "容器 toodeploy 微服務應用程式使用 Service Fabric 和 hello 的概觀。 本文章提供容器可以使用的方式，並 hello Service Fabric 中的可用功能的概觀。"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric 和容器
> [!NOTE]
> Linux 的這項功能處於預覽狀態。  部署 Windows 10 中的 tooa Service Fabric 叢集不支援的容器，但 （即將推出）。 
>   

## <a name="introduction"></a>簡介
Azure Service Fabric 是跨機器叢集的服務的 [Orchestrator](service-fabric-cluster-resource-manager-introduction.md)，在 Microsoft 的大規模服務中已使用多年且經過最佳化。 服務可以部署在許多方面，從使用 hello[程式設計模型的 Service Fabric](service-fabric-choose-framework.md) toodeploying[客體可執行檔](service-fabric-deploy-existing-app.md)。 根據預設，Service Fabric 會以處理序形式部署和啟動這些服務。 處理程序提供 hello 最快速的啟動和密度使用量最高的 hello 叢集中的資源。 Service Fabric 也可以在容器映像中部署服務。 重要的是，您可以混合在 hello 容器中處理序中的服務和服務相同的應用程式。 

## <a name="containers-and-service-fabric-roadmap"></a>容器和 Service Fabric 藍圖
在未來推出的版本中，針對容器協調流程和 Service Fabric 有許多改進計劃。 包含增強的網路功能以支援應用程式內的虛擬網路、安全性功能、改良的診斷功能和工具支援。 服務網狀架構可讓您混用的服務使用 hello Service Fabric 程式設計模型開發的封裝與現有的程式碼 （例如，IIS MVC 應用程式） 的容器 toocreate 應用程式。  您可以在單一叢集上執行數個這類應用程式。 

## <a name="what-are-containers"></a>什麼是容器？
容器封裝，以隔離的執行個體的個別部署元件 hello 作業系統提供的虛擬化相同核心 tootake 優點。 因此，每個應用程式和其執行階段、 相依性，以及系統程式庫執行容器內的作業系統建構完整的私用存取 toohello 容器自己隔離的檢視。 可攜性，此安全性和資源隔離程度會 hello 主要權益，適用於使用以 Service Fabric，這是其他處理序中執行服務的容器。

容器是虛擬化 hello 基礎作業系統與應用程式的虛擬化技術。 容器會提供有不同程度的隔離的應用程式 toorun 是不可變的環境。 容器會直接在 hello 核心之上執行，而且 hello 檔案系統的個別的檢視和其他資源。 比較的 toovirtual 機器容器具有下列優點 hello:

* **小型**： 容器會使用單一儲存體空間和圖層版本和更新 tooincrease 效率。
* **快速**： 容器沒有 tooboot 整個作業系統，因此他們可以啟動快得多，通常以秒為單位。
* **可攜性**： 進行容器化應用程式映像可以是移植的 toorun hello 雲端，在內部部署虛擬機器內，或直接在實體電腦上。
* **資源監管**： 容器可以限制 hello 可取其主機的實體資源。

## <a name="container-types"></a>容器類型
Service Fabric 支援 Linux 和 Windows 上的容器，也支援 hello 後者中的 HYPER-V 隔離模式。 

### <a name="docker-containers-on-linux"></a>Linux 上的 Docker 容器
Docker 提供高層級的應用程式開發介面 toocreate 和管理 Linux 核心容器頂端的容器。 Docker Hub 是中央儲存機制 toostore，和擷取容器映像。
如需教學課程，請參閱[部署 Docker 容器 tooService 網狀架構](service-fabric-get-started-containers-linux.md)。

### <a name="windows-server-containers"></a>Windows Server 容器
Windows Server 2016 提供兩種不同的 hello 提供隔離層級中不同的容器。 Windows Server 容器和 Docker 容器是類似，因為兩者都有命名空間和檔案系統的隔離，但共用 hello 核心與 hello 主機執行。 在 Linux 上，一向是由 `cgroups` 和 `namespaces` 提供這種隔離，而 Windows Server 容器具有類似的行為。

Windows HYPER-V 容器會提供更多隔離和安全性，因為每個容器不會與其他容器或 hello 主機共用 hello 作業系統核心。 由於有如此高程度的安全性隔離，Hyper-V 容器在惡意多租用戶的情況下是重點部分。
如需教學課程，請參閱[部署 Windows 容器 tooService 網狀架構](service-fabric-get-started-containers.md)。

hello 下圖顯示 hello 不同類型的 hello 作業系統中可用的虛擬化及隔離等級。
![Service Fabric 平台][Image1]

## <a name="scenarios-for-using-containers"></a>容器使用案例
以下是典型範例，容器是很好的選擇︰

* **IIS 提起和移位**： 如果您有現有的[ASP.NET MVC](https://www.asp.net/mvc)您希望 toocontinue toouse 應用程式將它們放在容器，而不是移轉它們 tooASP.NET 核心。 這些 ASP.NET MVC 應用程式相依於網際網路資訊服務 (IIS)。 您可以封裝到容器映像從預先建立 IIS 映像的 hello 這些應用程式，並將其部署以 Service Fabric。 請參閱[Windows Server 上的容器映像](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images)如需有關資訊 toocreate IIS 映像。
* **混合容器和 Service Fabric 微服務**︰針對您的應用程式的一部分使用現有的容器映像。 例如，您可能會使用 hello [NGINX 容器](https://hub.docker.com/_/nginx/)hello web 前端的應用程式和可設定狀態服務的 hello 更大量的後端計算。
* **減少 「 雜訊的鄰近項目 」 服務的影響**： 您可以使用的服務使用的主機的容器 toorestrict hello 資源 hello 資源控管能力。 如果服務可能會耗用許多資源，並會影響其他人 （例如長時間執行的查詢類似的作業） 的 hello 效能，請考慮將這些服務放入容器資源管理。

## <a name="service-fabric-support-for-containers"></a>Service Fabric 的容器支援
目前，Service Fabric 支援將 Docker 容器部署在 Linux，也支援將 Windows Server 容器部署在 Windows Server 2016 以及支援 Hyper-V 隔離模式。 

在 hello Service Fabric[應用程式模型](service-fabric-application-model.md)，容器代表複本會放在哪一種多個服務應用程式主機。 Service Fabric 可以執行任何容器，而 hello 案例是類似 toohello[客體可執行檔案例](service-fabric-deploy-existing-app.md)、 您用來封裝位在容器內現有的應用程式。 此案例中是 hello 常見使用案例的容器，並執行使用任何語言或架構，但不使用 hello 內建 Service Fabric 程式設計模型撰寫的應用程式的範例包括。

此外，您也可以執行容器內的 Service Fabric 服務。 目前，但 toobe 增強推出的版本中受到支援，在容器內執行的 Service Fabric 服務。

* **可靠的無狀態服務，在容器內**： 可靠無狀態服務使用的程式設計模型才支援在 Linux hello 可靠的服務。 未來版本計劃將增加支援 Windows 容器中的無狀態可靠服務。
* **在容器內的可設定狀態服務**： 這些服務使用 hello Reliable Actors 或可靠的服務程式設計模型。 未來版本中將增加支援容器中執行的具狀態服務。

Service Fabric 有數個容器功能可協助您建置由容器化微服務組成的應用程式。 Service Fabric 提供下列功能的容器化服務的 hello:

* 容器映像部署和啟用。
* 資源管理。
* 儲存機制驗證。
* 容器連接埠 toohost 連接埠對應。
* 容器至容器的探索及通訊。
* 能力 tooconfigure 並設定環境變數。

## <a name="next-steps"></a>後續步驟
在本文中，您已了解容器、Service Fabric 是容器協調者，以及 Service Fabric 具有支援容器的功能。 在下一個步驟中，我們將介紹每個的 hello 功能 tooshow 範例您如何 toouse 它們。

[部署 Windows 容器 tooService 網狀架構上 Windows Server 2016](service-fabric-get-started-containers.md)

[部署 Docker 容器 tooService Linux 上的網狀架構](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
