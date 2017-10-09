## <a name="create-a-device-identity"></a>建立裝置識別

在本節中，您可以使用名為的 Node.js 工具[iot 中樞總管][ iot-hub-explorer] toocreate 裝置身分識別，在此教學課程。 裝置識別碼會區分大小寫。

1. 命令列環境中執行下列 hello:

    `npm install -g iothub-explorer@latest`

1. 然後，執行下列命令 toologin tooyour 中樞 hello。 替代`{iot hub connection string}`以 hello 您先前複製的 IoT 中樞連接字串：

    `iothub-explorer login "{iot hub connection string}"`

1. 最後，建立新的裝置身分識別稱為`myDeviceId`hello 命令：

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

記下 hello 結果中的 hello 裝置連接字串。 這個裝置的連接字串會使用為裝置 hello 裝置應用程式 tooconnect tooyour IoT 中樞。

![][img-identity]

請參閱太[入門 IoT 中樞][ lnk-getstarted] tooprogrammatically 建立裝置身分識別。

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
