## <a name="create-a-device-identity"></a><span data-ttu-id="f4a17-101">建立裝置識別</span><span class="sxs-lookup"><span data-stu-id="f4a17-101">Create a device identity</span></span>

<span data-ttu-id="f4a17-102">在本節中，您可以使用名為的 Node.js 工具[iot 中樞總管][ iot-hub-explorer] toocreate 裝置身分識別，在此教學課程。</span><span class="sxs-lookup"><span data-stu-id="f4a17-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="f4a17-103">裝置識別碼會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="f4a17-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="f4a17-104">命令列環境中執行下列 hello:</span><span class="sxs-lookup"><span data-stu-id="f4a17-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="f4a17-105">然後，執行下列命令 toologin tooyour 中樞 hello。</span><span class="sxs-lookup"><span data-stu-id="f4a17-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="f4a17-106">替代`{iot hub connection string}`以 hello 您先前複製的 IoT 中樞連接字串：</span><span class="sxs-lookup"><span data-stu-id="f4a17-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="f4a17-107">最後，建立新的裝置身分識別稱為`myDeviceId`hello 命令：</span><span class="sxs-lookup"><span data-stu-id="f4a17-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="f4a17-108">記下 hello 結果中的 hello 裝置連接字串。</span><span class="sxs-lookup"><span data-stu-id="f4a17-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="f4a17-109">這個裝置的連接字串會使用為裝置 hello 裝置應用程式 tooconnect tooyour IoT 中樞。</span><span class="sxs-lookup"><span data-stu-id="f4a17-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="f4a17-110">請參閱太[入門 IoT 中樞][ lnk-getstarted] tooprogrammatically 建立裝置身分識別。</span><span class="sxs-lookup"><span data-stu-id="f4a17-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
