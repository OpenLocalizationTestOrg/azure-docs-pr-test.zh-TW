---
title: "與 Azure IoT 中樞 aaaDevice 管理 |Microsoft 文件"
description: "Azure IoT 中樞的裝置管理概觀︰企業裝置生命週期及裝置管理模式，例如重新啟動、恢復出廠預設值、韌體更新、設定、裝置對應項、查詢、作業。"
services: iot-hub
documentationcenter: 
author: bzurcher
manager: timlt
editor: 
ms.assetid: a367e715-55f6-4593-bd68-7863cbf0eb81
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: briz
ms.openlocfilehash: 7e22fb6eb3c541a513b16a047c7c3ef557255532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-device-management-with-iot-hub"></a>IoT 中樞的裝置管理概觀
## <a name="introduction"></a>簡介
Azure IoT 中樞提供 hello 功能和擴充性模型，可讓裝置與後端開發人員 toobuild 強固的裝置管理解決方案。 從受條件約束的感應器和單一用途微、 toopowerful 閘道路由群組的裝置通訊的裝置範圍。  此外，hello 使用案例和需求 IoT 運算子會大大地改變產業。  儘管這個變異中，與 IoT 中樞的裝置管理提供 hello 功能、 模式和程式碼程式庫 toocater tooa 多樣的裝置和使用者。

建立企業成功 IoT 解決方案的一個重要部分是 tooprovide 運算子如何處理 hello 持續管理他們的裝置集合的策略。 IoT 運算子需要簡單又可靠的工具和應用程式可讓它們在 hello toofocus 多個工作的策略部分。 本文提供：

* Azure IoT Hub 方法 toodevice 管理簡要概觀。
* 常見裝置管理原則的說明。
* Hello 裝置生命週期的描述。
* 常見裝置管理模式的概觀。

## <a name="device-management-principles"></a>裝置管理原則
IoT 會伴隨著一組唯一的裝置管理方面的挑戰和每個企業級解決方案必須解決下列原則 hello:

![裝置管理原則圖形][img-dm_principles]

* **小數位數和自動化**: IoT 解決方案需要簡單的工具，可以自動化例行工作，並讓較小的作業人員 toomanage 數以百萬計的裝置。 日運算子預期 toohandle 裝置作業遠端大量，並且 tooonly 需要直接注意發生問題時收到警示。
* **開放性和相容性**: hello 裝置生態系統是 hierarchy 不同。 管理工具必須是量身訂做的 tooaccommodate 到許多裝置類別、 平台及通訊協定。 運算子必須要能 toosupport 許多類型的裝置，從 hello 最限制內嵌單一處理序晶片、 toopowerful 和完全正常運作的電腦。
* **內容感知**：IoT 環境是動態且不斷變化的， 因此服務可靠性非常重要。 裝置管理作業，必須考慮下列因素 tooensure 帳戶 hello，維護停機時間並不重要的商務作業的影響，或建立危險情況：
    * SLA 維護期間
    * 網路和電源狀態
    * 使用中狀況
    * 裝置地理位置
* **服務的許多角色**: hello 唯一的工作流程和 IoT 操作角色中的處理序的支援很重要。 hello 操作人員必須與條件約束內部的 IT 部門的 hello harmoniously 合作。  它們也必須尋找持續性方式 toosurface 即時裝置作業資訊 toosupervisors 和其他商務管理角色。

## <a name="device-lifecycle"></a>裝置的生命週期
沒有一組通用 tooall 企業 IoT 專案的一般裝置管理階段。 在 Azure IoT 有 hello 裝置生命週期中的五個階段：

![hello 五個 Azure IoT 裝置生命週期階段： 規劃、 佈建、 設定、 監視、 淘汰][img-device_lifecycle]

在每個這些五個階段中，有數個裝置運算子需求，應該履行的 tooprovide 完整的解決方案：

* **計劃**： 啟用運算子 toocreate tooeasily 且精確地查詢，讓他們的裝置中繼資料配置，並以群組為目標的裝置進行大量管理作業。 您可以使用 hello 裝置兩個 toostore hello 表單的標記和屬性在此裝置中繼資料。
  
    *進一步閱讀*:[開始使用裝置雙][lnk-twins-getstarted]，[了解裝置雙][lnk-twins-devguide]，[方式toouse 裝置兩個屬性][lnk-twin-properties]。
* **佈建**： 安全地佈建新裝置 tooIoT 中樞，並啟用運算子 tooimmediately 探索裝置的功能。  使用 hello IoT 中樞身分識別登錄 toocreate 彈性裝置身分識別和認證，並執行這項作業中的大量使用作業。 建立裝置 tooreport，其功能與經由 hello 裝置兩個在裝置內容的條件。
  
    *進一步閱讀*:[管理裝置身分識別][lnk-identity-registry]，[大量的裝置身分識別管理][lnk-bulk-identity]， [Toouse 裝置如何 twin 屬性][lnk-twin-properties]。
* **設定**： 簡化大量組態變更和韌體更新 toodevices 維持健康情況與安全性。 使用所需的屬性或透過直接方法和廣播作業，大量執行這些裝置管理作業。
  
    *進一步閱讀*:[使用直接的方法][lnk-c2d-methods]，[叫用的裝置上直接方法][lnk-methods-devguide]，[方式toouse 裝置兩個屬性][lnk-twin-properties]，[排程和廣播的工作][lnk-jobs]， [的多個裝置上的工作排程][lnk-jobs-devguide].
* **監視**： 監視整體的裝置集合健全狀況、 hello 狀態，持續進行的作業，以及警示的操作員 tooissues 可能需要注意。  套用 hello 裝置兩個 tooallow 裝置 tooreport 即時操作條件和更新作業的狀態。 使用裝置的兩個查詢來建立功能強大的儀表板報表該介面的 hello 最立即的問題。
  
    *進一步閱讀*: [toouse 裝置如何 twin 屬性][lnk-twin-properties]，[裝置雙、 作業和訊息路由的 IoT 中樞查詢語言][lnk-query-language].
* **淘汰**： 取代或在失敗之後解除委任的裝置，請升級循環，或在 hello hello 服務的存留期的結尾。  如果 hello 實體裝置正在使用 hello 裝置兩個 toomaintain 裝置資訊被取代，或者若要淘汰封存。 使用 hello IoT 中樞身分識別登錄的安全地撤銷裝置身分識別與認證。
  
    *進一步閱讀*: [toouse 裝置如何 twin 屬性][lnk-twin-properties]，[管理裝置身分識別][lnk-identity-registry]。

## <a name="device-management-patterns"></a>裝置管理模式
IoT 中樞可讓 hello 遵循一組的裝置管理模式。  hello[裝置管理教學課程][ lnk-get-started]如何在更詳細地顯示 tooextend 這些模式 toofit 您確切的案例及如何 toodesign 新模式根據這些核心範本。

* **重新開機**-hello 後端應用程式會通知 hello 裝置透過直接的方法，它已起始重新開機。  hello 裝置使用 hello 報告屬性 tooupdate hello 的 hello 裝置的重新啟動狀態。
  
    ![裝置管理重新啟動模式圖形][img-reboot_pattern]
* **原廠重設**-hello 後端應用程式會通知 hello 裝置透過直接的方法，它具有起始原廠重設。  hello 裝置使用 hello 報告屬性 tooupdate hello 原廠重設 hello 裝置的狀態。
  
    ![裝置管理恢復出廠預設值模式圖形][img-facreset_pattern]
* **組態**-hello 後端應用程式會使用所需的 hello 屬性 tooconfigure 軟體 hello 裝置上執行。  hello 裝置使用 hello 回報 hello 裝置屬性 tooupdate 組態狀態。
  
    ![裝置管理設定模式圖形][img-config_pattern]
* **韌體更新**-hello 後端應用程式會通知 hello 裝置透過直接的方法，它具有起始軔體更新。  hello 裝置啟始包含多個步驟的程序 toodownload hello 的韌體映像、 套用 hello 的韌體映像，以及最後重新連線 toohello IoT 中樞服務。  在 hello 包含多個步驟程序 hello 裝置使用 hello 報告屬性 tooupdate hello 進度和 hello 裝置的狀態。
  
    ![裝置管理韌體更新模式圖形][img-fwupdate_pattern]
* **報告進度和狀態**-hello 方案後端執行裝置的兩個查詢，跨一組裝置、 tooreport hello 狀態和進度的 hello 裝置上執行的動作。
  
    ![裝置管理報告進度和狀態模式圖形][img-report_progress_pattern]

## <a name="next-steps"></a>後續步驟
hello 功能、 模式與 IoT 中樞提供裝置管理的程式碼程式庫可讓您在各個裝置生命週期階段滿足企業 IoT 運算子需求 toocreate IoT 應用程式。

toocontinue 深入了解在 IoT 中樞 hello 裝置管理功能，請參閱 「 hello[開始使用 裝置管理][ lnk-get-started]教學課程。

<!-- Images and links -->
[img-dm_principles]: media/iot-hub-device-management-overview/image4.png
[img-device_lifecycle]: media/iot-hub-device-management-overview/image5.png
[img-config_pattern]: media/iot-hub-device-management-overview/configuration-pattern.png
[img-facreset_pattern]: media/iot-hub-device-management-overview/facreset-pattern.png
[img-fwupdate_pattern]: media/iot-hub-device-management-overview/fwupdate-pattern.png
[img-reboot_pattern]: media/iot-hub-device-management-overview/reboot-pattern.png
[img-report_progress_pattern]: media/iot-hub-device-management-overview/report-progress-pattern.png

[lnk-twins-devguide]: iot-hub-devguide-device-twins.md
[lnk-get-started]: iot-hub-node-node-device-management-get-started.md
[lnk-twins-getstarted]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-hub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-query-language]: iot-hub-devguide-query-language.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-methods-devguide]: iot-hub-devguide-direct-methods.md
[lnk-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-jobs-devguide]: iot-hub-devguide-jobs.md
