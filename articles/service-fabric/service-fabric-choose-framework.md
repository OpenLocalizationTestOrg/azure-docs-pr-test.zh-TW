---
title: "aaaService 網狀架構程式設計模型概觀 |Microsoft 文件"
description: "Service Fabric 提供這兩個架構來建置服務： hello 動作項目架構並 hello 服務架構。 它們在簡化與控制中提供不同的取捨。"
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a>Service Fabric 程式設計模型概觀
Service Fabric 提供多個方式 toowrite 並管理您的服務。 服務可選擇 toouse hello 服務網狀架構 Api tootake 充分善用 hello 平台的功能和應用程式架構。 服務也可以是以任何語言撰寫的任何已編譯可執行程式，或是在 Service Fabric 叢集所裝載之容器中執行的程式碼。

## <a name="guest-executables"></a>客體可執行檔
[客體可執行檔](service-fabric-deploy-existing-app.md)是可在應用程式中作為服務執行的現有任意可執行檔 (以任何語言撰寫)。 客體可執行檔不直接呼叫 hello Service Fabric SDK Api。 不過他們仍然可以享受功能 hello 平台提供，例如服務探索功能、 自訂健全狀況和報告藉由呼叫 REST Api 服務的網狀架構所公開的負載。 它們也具備完整的應用程式生命週期支援。

部署您的第一個 [來賓可執行的應用程式](service-fabric-deploy-existing-app.md)，開始使用來賓可執行檔。

## <a name="containers"></a>容器
根據預設，Service Fabric 會以處理程序形式部署和啟用這些服務。 Service Fabric 也可以在[容器](service-fabric-containers-overview.md)中部署服務。 Service Fabric 支援在 Windows Server 2016 上部署 Linux 容器和 Windows 容器。 可以從任何容器儲存機制提取並部署 toohello 機器容器映像。 您可以將現有的應用程式部署為來賓 exectuables，Service Fabric 無狀態或狀態可靠的服務或 Reliable Actors 的容器，以及您可以混合使用處理序中的服務和服務中的容器中的 hello 相同的應用程式。

[深入了解如何在 Windows 或 Linux 中將服務容器化](service-fabric-deploy-container.md)

## <a name="reliable-services"></a>Reliable Services
可靠的服務是輕量級架構的撰寫與 hello Service Fabric 平台整合，並受益於 hello 組完整的平台功能的服務。 可靠的服務提供最基本的應用程式開發介面可讓 hello Service Fabric 執行階段 toomanage hello 的生命週期服務，以及可讓您的服務 toointeract hello 執行階段。 是最小的 hello 應用程式架構，讓您完整控制設計和實作的選項，而且可以使用的 toohost 任何其他應用程式架構，例如 ASP.NET Core。

可靠的服務可以是無狀態，類似 toomost 服務平台，例如 web 伺服器，在其中均等建立 hello 服務的每個執行個體和狀態會持續保留在外部的解決方案，例如 Azure DB 或 Azure 資料表儲存體。

可靠的服務也可以是可設定狀態、 獨佔 tooService 網狀架構，其中保存直接在 hello 服務本身使用可靠的集合中的狀態。 狀態透過複寫變得高度可用，並透過資料分割散發，全由 Service Fabric 自動管理。

[深入了解 Reliable Services](service-fabric-reliable-services-introduction.md)或從[撰寫第一個 Reliable Services](service-fabric-reliable-services-quick-start.md) 開始。

## <a name="reliable-actors"></a>Reliable Actors
Hello Reliable Actor 架構之上可靠的服務，是一種應用程式架構，以實作 hello Virtual Actor 模式，根據 hello 執行者設計模式。 hello Reliable Actor framework 會使用稱為執行者的單一執行緒執行獨立的單位計算和狀態。 hello Reliable Actor 架構提供執行者與預先設定的狀態持續性和向外延展設定的內建的通訊。

Reliable Actors 本身是建置在可靠的服務應用程式架構，因為它會完全整合 hello Service Fabric 平台與 hello hello 平台所提供的功能的一組完整的利益。

[深入了解 Reliable Actors](service-fabric-reliable-actors-introduction.md) 或從[撰寫第一項 Reliable Actor 服務](service-fabric-reliable-actors-get-started.md)開始

## <a name="aspnet-core"></a>ASP.NET Core
Service Fabric 與 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 整合，建置可以是應用程式一部分的 Web 和 API 服務。 

[使用 ASP.NET Core 組建前端服務](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a>後續步驟
[Service Fabric 和容器概觀](service-fabric-containers-overview.md)

[Reliable Services 概觀](service-fabric-reliable-services-introduction.md)

[Reliable Services 概觀](service-fabric-reliable-actors-introduction.md)

[Service Fabric 和 ASP.NET Core ](service-fabric-reliable-services-communication-aspnetcore.md)




