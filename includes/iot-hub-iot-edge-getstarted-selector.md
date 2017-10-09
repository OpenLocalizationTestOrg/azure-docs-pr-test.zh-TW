> [!div class="op_single_selector"]
> * [Linux](../articles/iot-hub/iot-hub-linux-iot-edge-get-started.md)
> * [Windows](../articles/iot-hub/iot-hub-windows-iot-edge-get-started.md)
> 
> 

本文章提供詳細的逐步解說的 hello [Hello World 範例程式碼][ lnk-helloworld-sample] tooillustrate hello 的基礎元件 hello [Azure IoT 邊緣][lnk-iot-edge]架構。 hello 範例會使用 hello Azure IoT 邊緣 toobuild 記錄"hello world"訊息 tooa 檔每五秒的簡單閘道。

本逐步解說涵蓋下列項目：

* **Hello World 範例架構**： 描述如何[Azure IoT 邊緣架構概念][ lnk-edge-concepts]套用 toohello Hello World 範例與 hello 元件一起。
* **如何 toobuild hello 範例**: hello 步驟需要的 toobuild hello 範例。
* **如何 toorun hello 範例**: hello 步驟需要的 toorun hello 範例。 
* **一般輸出**: hello 的範例輸出 tooexpect，當您執行 hello 範例。
* **程式碼片段**： 集合的程式碼片段 tooshow hello Hello World 範例如何實作主要 IoT 邊緣閘道元件。


## <a name="hello-world-sample-architecture"></a>Hello World 範例架構
hello Hello World 範例說明 hello 概念 hello 上一節中所述。 hello Hello World 範例會實作兩個 IoT 邊緣模組所組成的管線 IoT 邊緣閘道：

* hello *hello world*模組建立每五秒的訊息，並將其傳遞 toohello 記錄器模組。
* hello*記錄器*模組寫入 hello 訊息接收 tooa 檔案。

![使用 Azure IoT Edge 所建置之 Hello World 範例的架構][4]

Hello 上一節所述，模組未通過的 Hello World hello 訊息直接 toohello 記錄器模組每五秒。 相反地，發行訊息 toohello broker 每五秒。

hello 記錄器模組從 hello 代理人收到 hello 訊息，並可運作時，寫入 hello 的 hello 訊息 tooa 檔案的內容。

hello 記錄器模組只會消耗 hello broker 的訊息，永遠不會將發佈新訊息 toohello broker。

![Hello broker 將模組中 Azure IoT 邊緣之間的訊息的路由][5]

hello 上圖顯示 hello 架構 hello Hello World 範例與 hello 相對路徑 toohello 原始程式檔在 hello 實作不同部分的 hello 範例[儲存機制][lnk-iot-edge]。 自行瀏覽 hello 程式碼，或使用 hello 如下的程式碼片段做為指南。

<!-- Images -->
[4]: media/iot-hub-iot-edge-getstarted-selector/high_level_architecture.png
[5]: media/iot-hub-iot-edge-getstarted-selector/detailed_architecture.png

<!-- Links -->
[lnk-helloworld-sample]: https://github.com/Azure/iot-edge/tree/master/samples/hello_world
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-edge-concepts]: ../articles/iot-hub/iot-hub-iot-edge-overview.md