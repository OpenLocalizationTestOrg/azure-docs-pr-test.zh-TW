---
title: "Azure 服務匯流排中的 AMQP 1.0 aaaOverview |Microsoft 文件"
description: "了解如何使用 hello 進階訊息佇列通訊協定 (AMQP) 1.0 在 Azure 中。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0e8d19cc-de36-478e-84ae-e089bbc2d515
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: c35a20c50dd24845d9a4c7a0251e8240848a6f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-support-in-service-bus"></a>服務匯流排中的 AMQP 1.0 支援
同時 hello Azure 服務匯流排雲端服務和內部[Service Bus for Windows Server (服務匯流排 1.1)](https://msdn.microsoft.com/library/dn282144.aspx)支援 hello 進階訊息佇列通訊協定 (AMQP) 1.0。 AMQP 可讓您 toobuild 跨平台，使用開放標準的通訊協定的混合式應用程式。 您可以透過使用不同語言和架構所建立，且在不同作業系統上執行的元件來建構應用程式。 所有這些元件可以連接 tooService 匯流排，然後順暢地交換結構化的商業訊息，有效率地和完整不失真。

## <a name="introduction-what-is-amqp-10-and-why-is-it-important"></a>簡介：何謂 AMQP 1.0 以及它為什麼很重要？
傳統上，訊息導向的中介軟體產品會採用專屬的通訊協定，以進行用戶端應用程式和代理程式之間的通訊。 這表示，一旦您已選取特定供應商的訊息代理人，您必須使用該廠商的文件庫 tooconnect 您的用戶端應用程式 toothat broker。 這會導致該廠商，相依性程度，因為移植應用程式 tooa 不同產品需要所有的 hello 連線應用程式中的程式碼變更。 

此外，從不同廠商連接訊息代理程式有些麻煩。 這通常需要從一個系統 tooanother 和其專屬的訊息格式間 tootranslate 應用程式層級橋接 toomove 訊息。 這是常見的需求。例如，當您必須提供新的統一的介面 tooolder 不同的系統，或整合遵循合併的 IT 系統。

hello 軟體產業是快速移動企業;有時會令人困擾的步調引進新的程式設計語言和應用程式架構。 同樣地，IT 系統的 hello 需求隨著時間持續發展，開發人員想 tootake hello 最新的平台功能的優點。 不過，有時候 hello 選傳訊廠商不支援這些平台。 由於傳訊通訊協定是專屬的不供其他人可能 tooprovide 這些新的平台的程式庫。 因此，您必須使用如建置閘道或讓您的橋接器 toocontinue toouse hello 訊息產品的方法。

hello 的 hello 進階訊息佇列通訊協定 (AMQP) 1.0 基於這些問題的開發。 AMQP 是 JP Morgan Chase 的發明，與大多數的金融服務公司一樣，JP Morgan Chase 是訊息導向中介軟體的重度使用者。 hello 目標是簡單： toocreate 開放式標準訊息通訊協定，可讓可能 toobuild 訊息使用的應用程式元件使用不同的語言、 架構及作業系統來建置所有使用中的最佳品種元件供應商的範圍。

## <a name="amqp-10-technical-features"></a>AMQP 1.0 技術功能
AMQP 1.0 是一種有效率、 可靠、 有線等級訊息通訊協定，您可以使用 toobuild 強固、 跨平台訊息應用程式。 hello 通訊協定有簡單的目標： hello 安全、 可靠且有效率的訊息傳輸兩個合作對象之間的 toodefine hello 機制。 hello 訊息本身是使用可攜式資料表示法，讓異質傳送者和接收者 tooexchange 結構化的商務訊息臨場感來編碼。 hello 下面是 hello 最重要功能的摘要：

* **有效率**: AMQP 1.0 是連線導向的通訊協定使用二進位編碼 hello 通訊協定指示和 hello 透過其傳輸的商務訊息。 其中包含精密的流程控制配置 toomaximize hello 使用量 hello 網路與 hello 連接元件。 話雖如此，hello 通訊協定已設計的 toostrike 效率、 彈性及交互操作性之間取得平衡。
* **可靠**: hello AMQP 1.0 通訊協定可讓與某個範圍的可靠性保證，和不理 tooreliable，從完全交換的訊息 toobe-認可一次的傳遞。
* **彈性**: AMQP 1.0 是彈性的通訊協定可以使用的 toosupport 不同拓撲。 hello 相同的通訊協定可以用於用戶端、 用戶端-broker 與 broker 與 broker 通訊。
* **與代理人模型無關**: hello AMQP 1.0 規格不會在代理人使用的 hello 訊息模型上的任何需求。 這表示它是可能 tooeasily 新增 AMQP 1.0 支援 tooexisting 傳訊代理程式。

## <a name="amqp-10-is-a-standard-with-a-capital-s"></a>AMQP 1.0 是一項標準 (Standard 的 S 為大寫)
AMQP 1.0 是由 ISO 與 IEC 核定為 ISO/IEC 19464:2014 的國際標準。

有一個由包含技術提供者及使用者公司在內超過 20 家公司所組成的核心群組，從 2008 年起就開始開發 AMQP 1.0。 在這段時間，使用者公司有貢獻真實世界的商業需求並 hello 技術廠商進化 hello 通訊協定 toomeet 這些需求。 在整個 hello 程序，廠商參與了的研討會，它們共同作業 toovalidate hello 他們實作間的交互操作性。

在 October 2011 hello 的開發工作轉換 tooa 技術委員會 hello 組織 hello 先進的結構化 Information Standards (OASIS) 內，於 2012 年 10 月發行 hello OASIS AMQP 1.0 標準。 hello 下列公司在參與 hello 技術委員會 hello hello 標準開發期間：

* **技術廠商**：Axway Software、Huawei Technologies、IIT Software、INETCO Systems、Kaazing、Microsoft、Mitre Corporation、Primeton Technologies、Progress Software、Red Hat、SITA、Software AG、Solace Systems、VMware、WSO2、Zenika。
* **使用者公司**：Bank of America、Credit Suisse、Deutsche Boerse、Goldman Sachs、JPMorgan Chase。

某些 hello 常引用的開放式標準的優點包括：

* 比較不會被廠商鎖定
* 互通性
* 可以廣泛使用程式庫與工具
* 提供保護以免過時
* 對於有經驗之員工的可用性
* 較低且可管理的風險

## <a name="amqp-10-and-service-bus"></a>AMQP 1.0 和服務匯流排
Azure 服務匯流排中的 AMQP 1.0 支援表示您可以立即利用 hello Service Bus 佇列和發佈/訂閱代理傳訊功能從某個範圍的平台使用有效率的二進位通訊協定。 此外，您還可以建置使用混合語言、架構及作業系統所建置之元件所組成的應用程式。

hello 下圖說明使用 hello 標準的 Java 訊息服務 (JMS) API 撰寫的 Linux 上執行的 Java 用戶端和執行在 Windows 中，透過使用 AMQP 1.0 的服務匯流排交換訊息的.NET 用戶端部署範例。

![][0]

**圖 1：範例部署案例示範使用服務匯流排和 AMQP 1.0 的跨平台訊息服務**

在此時間 hello 下列用戶端程式庫是已知 toowork 具有服務匯流排：

| 語言 | 程式庫 |
| --- | --- |
| Java |Apache Qpid Java 訊息服務 (JMS) 用戶端<br/>IIT Software SwiftMQ Java 用戶端 |
| C |Apache Qpid Proton-C |
| PHP |Apache Qpid Proton-PHP |
| Python |Apache Qpid Proton-Python |
| C# |AMQP .Net Lite |

**圖 2：AMQP 1.0 用戶端程式庫的資料表**

## <a name="summary"></a>摘要
* AMQP 1.0 是一個開啟可靠傳訊通訊協定，您可以使用 toobuild 跨平台，混合式應用程式。 AMQP 1.0 是一項 OASIS 標準。
* Azure 服務匯流排和 Service Bus for Windows Server (Service Bus 1.1) 中現可支援 AMQP 1.0。 定價為的 hello 一樣 hello 現有通訊協定。

## <a name="next-steps"></a>後續步驟
更準備 toolearn 嗎？ 請造訪下列連結查看 hello:

* [搭配使用 .NET 的服務匯流排與 AMQP]
* [搭配使用 Java 的服務匯流排與 AMQP]
* [在 Azure Linux VM 上安裝 Apache Qpid Proton-C]
* [Windows Server 服務匯流排中的 AMQP]

[0]: ./media/service-bus-amqp-overview/service-bus-amqp-1.png
[搭配使用 .NET 的服務匯流排與 AMQP]: service-bus-amqp-dotnet.md
[搭配使用 Java 的服務匯流排與 AMQP]: service-bus-amqp-java.md
[在 Azure Linux VM 上安裝 Apache Qpid Proton-C]: service-bus-amqp-apache.md
[Windows Server 服務匯流排中的 AMQP]: https://msdn.microsoft.com/library/dn574799.aspx
