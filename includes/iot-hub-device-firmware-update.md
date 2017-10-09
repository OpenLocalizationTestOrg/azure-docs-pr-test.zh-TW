## <a name="create-a-simulated-device-app"></a><span data-ttu-id="8cf69-101">建立模擬裝置應用程式</span><span class="sxs-lookup"><span data-stu-id="8cf69-101">Create a simulated device app</span></span>
<span data-ttu-id="8cf69-102">在本節中，您可：</span><span class="sxs-lookup"><span data-stu-id="8cf69-102">In this section, you:</span></span>

* <span data-ttu-id="8cf69-103">建立回應 tooa 直接方法呼叫 hello 雲端 Node.js 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="8cf69-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="8cf69-104">觸發模擬韌體更新</span><span class="sxs-lookup"><span data-stu-id="8cf69-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="8cf69-105">使用 hello 回報屬性 tooenable 裝置兩個查詢 tooidentify 裝置和當他們最後一次完成韌體更新</span><span class="sxs-lookup"><span data-stu-id="8cf69-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="8cf69-106">步驟 1：建立稱為 **manageddevice** 的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="8cf69-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="8cf69-107">在 hello **manageddevice**資料夾中，建立使用下列命令，在您的命令提示字元的 hello package.json 檔案。</span><span class="sxs-lookup"><span data-stu-id="8cf69-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="8cf69-108">接受所有的 hello 預設值：</span><span class="sxs-lookup"><span data-stu-id="8cf69-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="8cf69-109">步驟 2： 在命令提示字元中 hello **manageddevice**資料夾中，執行下列命令 tooinstall hello hello **azure iot 裝置**和**azure iot 裝置-mqtt**裝置SDK 封裝：</span><span class="sxs-lookup"><span data-stu-id="8cf69-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="8cf69-110">步驟 3： 使用文字編輯器，建立**dmpatterns_fwupdate_device.js**檔案在 hello **manageddevice**資料夾。</span><span class="sxs-lookup"><span data-stu-id="8cf69-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="8cf69-111">步驟 4： 加入 hello 下列的 '需要' 陳述式在 hello 開頭的 hello **dmpatterns_fwupdate_device.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="8cf69-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="8cf69-112">步驟 5： 加入**connectionString**變數，並使用它 toocreate**用戶端**執行個體。</span><span class="sxs-lookup"><span data-stu-id="8cf69-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="8cf69-113">取代 hello`{yourdeviceconnectionstring}`預留位置 hello 您先前記下的 hello 「 建立裝置身分識別 」 一節中先前的連接字串：</span><span class="sxs-lookup"><span data-stu-id="8cf69-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="8cf69-114">步驟 6： 加入 hello 下列函式，是使用的 tooupdate 報告屬性：</span><span class="sxs-lookup"><span data-stu-id="8cf69-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

<span data-ttu-id="8cf69-115">步驟 7： 新增下列模擬下載並套用 hello 的韌體映像的函式的 hello:</span><span class="sxs-lookup"><span data-stu-id="8cf69-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

<span data-ttu-id="8cf69-116">步驟 8： 加入下列函式透過 hello 更新 hello 韌體更新狀態報告的屬性太 hello**等候**。</span><span class="sxs-lookup"><span data-stu-id="8cf69-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="8cf69-117">一般而言，裝置就會接到通知可用的更新和系統管理員定義的原則會導致 hello 裝置 toostart 下載並套用 hello 更新。</span><span class="sxs-lookup"><span data-stu-id="8cf69-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="8cf69-118">此函式是其中 hello 原則應該執行的邏輯 tooenable。</span><span class="sxs-lookup"><span data-stu-id="8cf69-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="8cf69-119">為了簡單起見，hello 範例等候再繼續 toodownload hello 的韌體映像之前的四個秒數：</span><span class="sxs-lookup"><span data-stu-id="8cf69-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

<span data-ttu-id="8cf69-120">步驟 9： 加入下列函式透過 hello 更新 hello 韌體更新狀態報告的屬性太 hello**下載**。</span><span class="sxs-lookup"><span data-stu-id="8cf69-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="8cf69-121">hello 函式接著會模擬韌體下載並更新最後 hello 韌體更新狀態 tooeither **downloadFailed**或**downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="8cf69-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

<span data-ttu-id="8cf69-122">步驟 10： 加入下列函式透過 hello 更新 hello 韌體更新狀態報告的屬性太 hello**套用**。</span><span class="sxs-lookup"><span data-stu-id="8cf69-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="8cf69-123">hello 函式接著會模擬套用 hello 的韌體映像並更新最後 hello 韌體更新狀態 tooeither **applyFailed**或**applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="8cf69-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

<span data-ttu-id="8cf69-124">步驟 11： 加入 hello 下列函式的控制代碼 hello **firmwareUpdate**直接的方法和啟始 hello 多階段韌體更新程序：</span><span class="sxs-lookup"><span data-stu-id="8cf69-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

<span data-ttu-id="8cf69-125">步驟 12： 最後，加入下列程式碼連接 tooyour IoT 中樞的 hello:</span><span class="sxs-lookup"><span data-stu-id="8cf69-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> <span data-ttu-id="8cf69-126">簡單 tookeep 方面，本教學課程未實作任何重試原則。</span><span class="sxs-lookup"><span data-stu-id="8cf69-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="8cf69-127">在實際執行程式碼，您應該實作重試原則 （例如指數型輪詢），做為建議 hello MSDN 文件中[暫時性錯誤處理](https://msdn.microsoft.com/library/hh675232.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8cf69-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 