---
title: "aaaAzure 函式耗用量和應用程式服務計劃 |Microsoft 文件"
description: "了解 Azure 函式如何縮放 toomeet hello 事件驅動工作負載的需求。"
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, webhook, 動態計算, 無伺服器架構"
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure Functions 取用和 App Service 方案 

## <a name="introduction"></a>簡介

Azure Functions 的執行模式有兩種︰取用方案和 Azure App Service 方案。 hello 耗用量計劃您的程式碼會執行時，能有效擴充為必要 toohandle 負載，而且再按比例減少 程式碼未執行時，自動配置運算能力。 因此，您沒有 toopay 閒置 Vm 的而且沒有 tooreserve 容量事先。 本文著重在 hello 耗用量計劃。 如需 hello 應用程式服務方案的運作方式的詳細資訊，請參閱 hello [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。 

如果您不熟悉 Azure 函式，請參閱 hello [Azure 函式概觀](functions-overview.md)。

當您建立函式的應用程式時，您必須設定主控方案函式包含該 hello 應用程式。 在任一模式中，執行個體的 hello *Azure 函式主機*執行 hello 函式。 hello 計劃的控制項類型：

* 主控件執行個體如何向外延展。
* hello 受到可用 tooeach 主機的資源。

目前，您必須在 hello hello 函式應用程式建立期間選擇 hello 計劃類型。 之後便無法更改。 

您可以在 hello 應用程式服務方案的各層之間進行調整。 Hello 耗用量計畫，Azure 函式會自動處理所有的資源配置。

## <a name="consumption-plan"></a>取用方案

當您使用的耗用量計劃時，hello Azure 函式主控件執行個體以動態方式加入和移除根據 hello 傳入的事件數目。 這個方案會自動調整，您只需支付您的函式執行時使用的計算資源。 在取用方案中，函式最多可執行 10 分鐘。 

> [!NOTE]
> hello 耗用量計劃的函式的預設逾時是 5 分鐘。 hello 值可以是藉由變更 hello 屬性的 hello 函式應用程式的增加的 too10 分鐘`functionTimeout`中[host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json)。

計費是根據執行時間和使用的記憶體，會針對函數應用程式內的所有函式加以彙總。 如需詳細資訊，請參閱 hello [Azure 函式定價頁面]。

hello 耗用量計劃是 hello 預設值，而且提供下列優點 hello:
- 只有當您的函式執行時才需付費。
- 自動調整規模，即使在高負載期間也會。

## <a name="app-service-plan"></a>App Service 方案

Basic、 Standard 和 Premium Sku 類似 tooWeb 應用程式上的專用 Vm 上執行的應用程式函式，在 hello 應用程式服務計劃。 專用的 Vm 是配置的 tooyour App Service 應用程式，也就是說 hello 函式主機持續執行。

請考慮在下列情況下的 hello App Service 方案：
- 您有現有的、使用量過低的 VM 已在執行其他 App Service 執行個體。
- 您預期您的函式的應用程式 toorun 持續，或幾乎持續。
- 您需要更多的 CPU 或記憶體選項所提供 hello 耗用量計劃。
- 您需要 toorun 超過 hello hello 耗用量計劃允許最大執行時間。

VM 會減少執行階段和記憶體大小的成本。 如此一來，您將支付超過您配置的 hello VM 執行個體的 hello 成本。 如需 hello 應用程式服務方案的運作方式的詳細資訊，請參閱 hello [Azure App Service 方案深入概觀](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。 

使用 App Service 方案時，您可以透過手動新增更多 VM 執行個體來相應放大，或者您可以啟用自動規模調整。 如需詳細資訊，請參閱[手動或自動調整執行個體計數規模](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json)。 您也可以透過選擇不同的 App Service 方案來相應增加。 如需詳細資訊，請參閱[在 Azure 中為應用程式進行相應增加](../app-service-web/web-sites-scale.md)。 如果您打算 toorun JavaScript 函式上的應用程式服務計劃，您應該選擇的方案有較少的核心。 如需詳細資訊，請參閱 hello [JavaScript 函式的參考](functions-reference-node.md#choose-single-core-app-service-plans)。  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###永遠開啟

如果您執行應用程式服務方案時，您應該啟用 hello **Always On**設定，好讓您的函式應用程式能夠正確執行。 App Service 方案，在 hello 函式執行階段會進入閒置狀態一段時間，請稍候幾分鐘讓只有 HTTP 觸發程序將 「 喚醒 」 函式。 這是類似 toohow WebJobs 必須已啟用 Always On。 

只有 App Service 方案具備「永遠開啟」選項。 耗用量計劃，hello 平台會自動啟動函式應用程式。

## <a name="storage-account-requirements"></a>儲存體帳戶的需求

不論是取用方案或 App Service 方案，函數應用程式都需要有支援 Azure Blob、佇列、表格儲存體的 Azure 儲存體帳戶。 Azure Functions 會在內部使用「Azure 儲存體」來進行作業，例如管理觸發程序和記錄函數執行。 有些儲存體帳戶並不支援佇列和表格，例如僅限 Blob 的儲存體帳戶 (包括進階儲存體) 和搭配區域備援儲存體複寫的一般用途儲存體帳戶。 這些帳戶會篩選從 hello**儲存體帳戶**刀鋒視窗中建立函數應用程式時。

toolearn 進一步了解儲存體帳戶類型，請參閱[簡介 hello Azure 儲存體服務](../storage/common/storage-introduction.md#introducing-the-azure-storage-services)。

## <a name="how-hello-consumption-plan-works"></a>Hello 耗用量計劃的運作方式

hello 耗用量計劃自動縮放透過加入其他執行個體的 hello 函式的主機，根據 hello 其函式觸發的事件數目的 CPU 和記憶體資源。 Hello 函式主控件的每個執行個體是記憶體的有限的 too1.5 GB。

當您使用 hello 裝載計劃的耗用量，hello 主要儲存體帳戶的 Azure 檔案共用上儲存函式的程式碼檔案。 當您刪除 hello 主要儲存體帳戶時，此內容會被刪除，且無法復原。

> [!NOTE]
> 當您使用的 blob 觸發程序消耗計劃時，可以有向上 tooa 10 分鐘的延遲處理新的 blob，如果函式應用程式已進入閒置狀態。 Hello 函式應用程式執行之後，blob 會立即處理。 此初始 tooavoid 延遲，請考慮下列選項的 hello 的其中一個：
> - 使用 App Service 方案並啟用「永遠開啟」。
> - 使用處理，例如包含 hello blob 名稱的佇列訊息另一個的機制 tootrigger hello blob。 如需範例，請參閱[具有 blob 輸入繫結的佇列觸發程序](functions-bindings-storage-blob.md#input-sample)。

### <a name="runtime-scaling"></a>執行階段調整

Azure 的函式會使用一種稱為 hello 元件*標尺控制器*toomonitor hello 事件的速率，並判斷是否 tooscale out 或向下調整。 hello 標尺控制器會使用啟發學習法，每個觸發程序類型。 例如，當您使用 Azure 佇列儲存體的觸發程序，它縮放根據 hello 佇列長度和 hello 最舊的佇列訊息的 hello 年齡。

標尺的 hello 單位為 hello 函式應用程式。 當 hello 函式應用程式會向外延展時，所需資源配置 toorun hello Azure 函式主控件的多個執行個體。 相反地，做為計算要求降低，hello 標尺控制器中移除函式主控件執行個體。 執行個體數目 hello 最終縮小 toozero 沒有函式函式的應用程式內執行時。

![縮放控制器能監視事件及建立執行個體](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>計費模式

計費的詳細說明 hello 耗用量計劃在 hello [Azure 函式定價頁面]。 使用方式在 hello 函式應用程式層級彙總資料，並且計算只有 hello 函式程式碼正在執行的時間。 hello 下面是計費單位： 
* **以十億位元組-秒 (GB-s) 為單位的資源取用量**。 會計算為在函數應用程式中執行之所有函式的記憶體大小和執行時間組合。 
* **執行**。 計算每個函式會在回應 tooan 觸發的事件，繫結程序中執行的時間。

[Azure 函式定價頁面]: https://azure.microsoft.com/pricing/details/functions
