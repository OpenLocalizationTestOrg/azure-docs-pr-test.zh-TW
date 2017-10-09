## <a name="associate-an-azure-storage-account-tooiot-hub"></a>建立關聯的 Azure 儲存體帳戶 tooIoT 中樞

由於 hello 模擬的裝置應用程式上傳檔案 tooa blob，您必須有[Azure 儲存體](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)帳戶相關聯 tooIoT 中樞。 當您建立 IoT 中樞與關聯的 Azure 儲存體帳戶時，hello IoT 中樞將會產生 SAS URI。 裝置可以使用此 SAS URI toosecurely 上傳檔案 tooa blob 容器。 hello IoT 中心服務和 hello 裝置 Sdk 協調 hello 程序，會產生 hello SAS URI，並使其可用 tooa 裝置 toouse tooupload 檔案。

請依照下列中的 hello 指示[使用 hello Azure 入口網站設定檔案上傳](../articles/iot-hub/iot-hub-configure-file-upload.md)tooassociate Azure 儲存體帳戶 tooyour IoT 中樞。 請確定 blob 容器與 IoT 中樞相關聯，並已啟用檔案通知。

![在入口網站中啟用檔案通知](media/iot-hub-associate-storage/enable-file-notifications.png)