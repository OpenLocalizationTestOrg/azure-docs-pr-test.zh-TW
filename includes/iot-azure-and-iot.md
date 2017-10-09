
# <a name="azure-and-internet-of-things"></a>Azure 和物聯網

歡迎使用 tooMicrosoft Azure 和 hello 物聯網 (IoT)。 本文介紹描述 hello 共同的特性，您可能會使用 Azure 服務來部署的 IoT 解決方案的 IoT 解決方案架構。 IoT 解決方案都需要保護，可能編號 hello 百萬和解決方案的後端中的裝置之間的雙向通訊。 比方說，解決方案的後端可能會使用自動化、 預測分析 toouncover insights 從您的裝置到雲端的事件資料流。

當您使用 Azure 服務實作此 IoT 解決方案架構時，Azure IoT 中樞是其中的重要建置組塊。 IoT 套件可針對特定的 IoT 案例端對端地完整實作這個架構。 例如：

* hello*遠端監視*解決方案可讓您的裝置，例如 vending 機器 toomonitor hello 狀態。
* hello*預測性維護*解決方案可協助您的裝置，例如在遠端的提取站台和 tooavoid 排程之外的停機時間幫浦 tooanticipate 維護需求。
* hello*連接的工廠*方案可協助您 tooconnect 和監視您工業的裝置。

## <a name="iot-solution-architecture"></a>IoT 解決方案架構

hello 下列圖表顯示一個典型的 IoT 解決方案架構。 hello 圖表不包含任何特定的 Azure 服務的 hello 名稱，但描述泛型的 IoT 解決方案架構中的 hello 重要元素。 在這種架構，IoT 裝置收集他們傳送 tooa 雲端閘道的資料。 hello 雲端閘道 hello 資料可讓資料傳送 tooother 特定業務應用程式或透過儀表板或其他簡報裝置 toohuman 運算子其他後端服務進行處理。

![IoT 解決方案架構][img-solution-architecture]

> [!NOTE]
> IoT 架構的深入討論，請參閱 hello [Microsoft Azure IoT 參考架構][lnk-refarch]。

### <a name="device-connectivity"></a>裝置連線能力

在此 IoT 解決方案架構中，裝置會傳送遙測，例如從提取的站台、 儲存體的 tooa 雲端端點的感應器讀數和處理。 在預測性維護案例中，當特定幫浦需要維護 hello 方案後端時，可能會使用感應器資料 toodetermine hello 資料流。 裝置也可以接收和回應 toocloud 到裝置訊息從雲端端點讀取訊息。 比方說，hello 預測性維護實例 hello 解決方案後端可能會傳送訊息 tooother 幫浦中提取站 toobegin 重設路徑操作流程維護到期之前的 hello toostart。 此程序可確保無法她到達時立即開始 hello 維護工程師。

其中一個 hello 面對 IoT 專案最大的挑戰是如何 tooreliably 安全地連線裝置 toohello 方案後端。 IoT 裝置做為比較的 tooother 用戶端，例如瀏覽器和行動裝置應用程式具有不同的特性。 IoT 裝置：

* 通常是無人操作的嵌入式系統。
* 可以部署於實體存取成本昂貴的遠端位置。
* 只能透過 hello 方案後端連線。 沒有任何其他方式 toointeract 與 hello 裝置。
* 能力和/或處理資源可能都有限。
* 網路連線能力可能不穩定、緩慢或昂貴。
* 可能需要 toouse 專用、 自訂或業界特定的應用程式通訊協定。
* 可以使用一組大型常見的硬體和軟體平台來建立。

除了上述 toohello 需求，任何 IoT 解決方案必須也提供小數位數、 安全性和可靠性。 hello 產生的連線需求是困難且耗時 tooimplement 使用傳統的技術，例如 web 容器和傳訊代理程式。 Azure IoT 中樞與 hello Azure IoT 裝置 Sdk 讓您更輕鬆 tooimplement 解決方案符合這些需求。

裝置可直接聯繫雲端閘道端點，或如果 hello 裝置無法使用任何 hello hello 雲端閘道支援的通訊協定，它可在透過中繼的閘道連線。 例如，hello [Azure IoT 通訊協定閘道][ lnk-protocol-gateway]可以執行轉換的通訊協定，如果裝置無法使用的任何 hello IoT 中心支援的通訊協定。

### <a name="data-processing-and-analytics"></a>資料處理和分析

Hello 雲端中的 IoT 解決方案後端大部分都是 hello 資料處理的例如篩選和彙總遙測和 tooother 服務路由傳送。 hello IoT 解決方案後端：

* 從您的裝置接收大規模的遙測，並決定如何 tooprocess 及儲存該資料。 
* 可讓您從 hello 雲端 toospecific 裝置 toosend 命令。
* Tooprovision 裝置和 toocontrol 哪些裝置允許 tooconnect tooyour 基礎結構，提供可讓您的裝置註冊功能。
* 可讓您 tootrack hello 您裝置的狀態，並監視其活動。

Hello 預測性維護案例中，hello 方案後端儲存歷程記錄的遙測資料。 hello 方案後端可以使用此資料 toouse tooidentify 模式 」，表示要維護到期日特定幫浦。

IoT 解決方案可以包含自動意見反應迴圈。 比方說，就可以從特定裝置 hello 溫度高於一般的作業系統層級的遙測識別 hello 方案後端中的分析模組。 hello 方案就可以傳送命令 toohello 裝置，指示它 tootake 矯正措施。

### <a name="presentation-and-business-connectivity"></a>簡報及商務連線

hello 展示和商業連線的層級可讓一般使用者，以 hello 的 IoT 解決方案 toointeract 和 hello 裝置。 它可讓使用者 tooview，並分析 hello 資料收集從他們的裝置。 這些檢視可以採用 hello 形式的儀表板或 BI 報表可以顯示兩個歷程記錄資料，或接近即時的資料。 比方說，操作員可以檢查特定幫浦的站台的 hello 狀態，並查看 hello 系統所發出的任何警示。 此圖層也可讓與現有的特定業務應用程式 tootie 的 hello IoT 解決方案後端整合到企業的商務程序或工作流程。 例如，hello 預測性維護方案可以整合排程系統該書籍工程師 toovisit 幫浦的站台時 hello 方案識別需要維護幫浦。

![IoT 解決方案儀表板][img-dashboard]

[img-solution-architecture]: ./media/iot-azure-and-iot/iot-reference-architecture.png
[img-dashboard]: ./media/iot-azure-and-iot/iot-suite.png

[lnk-machinelearning]: http://azure.microsoft.com/documentation/services/machine-learning/
[Azure IoT Suite]: http://azure.microsoft.com/solutions/iot
[lnk-protocol-gateway]:  ../articles/iot-hub/iot-hub-protocol-gateway.md
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
