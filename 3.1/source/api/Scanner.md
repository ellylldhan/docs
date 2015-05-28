#Scanner

Scanner class will represent and provides access to the physical scanner device.  

**Example Usage:**

	:::java
	Scanner scanner = barcodeManager.getDevice(DeviceIdentifer.DEFAULT); 
    scanner.enable(); 
    scanner.addDataListener(this); 
    scanner.read(); 
    scanner.cancelRead(); 
    scanner.disable();

**Version:**

1.0

##Public Methods
###addDataListener(Scanner.DataListener listener)
The client can register to get data notification via callbacks.

**Parameters:**

**listener** - The DataListener callabck object.

**Returns:**

void

###addStatusListener(Scanner.StatusListener listener)
The client can register to get status notification via callbacks.

**Parameters:**

**listener**

**Returns:**

void

###cancelRead()
This Cancels any pending asynchronous read() calls.

**Example Usage:**

	:::java
	scanner.cancelRead();

**Returns:**

void

**Throws:**

[ScannerException](ScannerException) - The exception will thrown if error occurs during the cancelRead request.

###disable()
Disables the scanner hardware. Any pending scanned data will be lost. This method releases the scanner hardware resources for other application to use. You must call this as soon as you're done with the scanning.

**Example Usage:**

    :::java
    scanner.disable();

**Returns:**

void

**Throws:**

[ScannerException](ScannerException) - The exception will thrown if the scanner disable fails.

###enable()
Enables the scanner hardware. This method does not make the scanner to scan or turn on the laser. If the same of scanner is enabled by other applications, this will throw ScannerExceptions. You must call disable() when you are done the scanning, otherwise it will remain locked and be unavailable to other applications. 

**Example Usage:**

    :::java
    scanner.enable();

**Returns:**

void

**Throws:**

[ScannerException](ScannerException) -  The exception will thrown if the scanner enable fails.

###getConfig()
Gets the current configuration settings for this scanner device. If modifications are made to the returned ScannerConfig object, the Scanner.setConfig(ScannerConfig) must be called to take effect. Scanner must be enabled before calling getConfig(). 

**Example Usage:**

    :::java
    scanner.enable(); 
    ScannerConfig config = scanner.getConfig();

**Returns:**

com.symbol.emdk.barcode.[ScannerConfig](ScannerConfig) - scannerConfig The valid scanner configuration object will be returned on successful get.

**Throws:**

[ScannerException](ScannerException)

###getInterfaceConfig() throws ScannerException

**Returns:**

[InterfaceConfig](BarcodeInterfaceConfig) object.

**Throws:**

[ScannerException](ScannerException)

###getScannerInfo()
Returns information about the scanner device. 

**Returns:**

com.symbol.emdk.barcode.[ScannerInfo](ScannerInfo) - Returns the ScannerInfo object.

###isEnabled() 

**Returns:**

boolean

###isReleased()
Returns scanner object state.

**Returns:**

boolean - boolean Object state.

###isReadPending()
Another read() cannot be submitted while a read is pending.

**Returns:**

boolean - Returns true if a read is pending.

###read()
Starts an asynchronous Scan. The method will not turn on the scanner. It will, however, put the scanner in a state in which the scanner can be turned ON either by pressing a hardware trigger or can be turned ON automatically. This is determined by the Scanner.triggerType. The data notification must be registered in order to scan and get the Scan Data. The read request can be cancelled by issuing a cancelRead.

If a read() is submitted while another read is pending, the method call will fail. It is recommended to  check whether a read is pending by calling isReadPending() before submitting a read(). A read() can also be submitted from within onData and onStatus events. If called within onStatus, it should be called only when IDLE status is received.  If called within onData, then checking for isReadPending() is recommended.

**Example Usage:**

    :::java
    scanner.read();

**Throws:**

[ScannerException](ScannerException) - The exception will thrown if error occurs during the read request.

**Returns:**

void

###removeDataListener(Scanner.DataListener listener)
The client can un-register to get data notification via callbacks.

**Parameters:**

**listener**

**Returns:**

void

###removeStatusListener(Scanner.StatusListener listener)
The client can un-register to get status notification via callbacks.

**Parameters:**

**listener**

**Returns:**

void

###setConfig(ScannerConfig scannerConfig)
Changes the settings for this scanner device. The unsupported parameters will be ignored. This method skips the unsupported parameters and continues with setting the supported values.

**Example Usage:**

    :::java
    ScannerConfig scannerConfig = scanner.getConfig();
    scannerConfig.scanParams.decodeLEDTime = 10; 
    scanner.setConfig(scannerConfig);

**Parameters:**

**scannerConfig** - The Parameters to use for this scanner device.

**Returns:**

void

**Throws:**

[ScannerException](ScannerException) - Exception will be throw if any error occurs while setting the parameters.

###setInterfaceConfig(InterfaceConfig interfaceConfig) throws ScannerException

**Returns:**

void

**Throws:**

[ScannerException](ScannerException)
  
##Public Fields
###triggerType
Specifies the trigger type for the scanner. It is set to HARD by default.

**Type:**

com.symbol.emdk.barcode.[Scanner.TriggerType](Scanner#Scanner.TriggerType)

##Public Enums
###Scanner.TriggerType
List of supported trigger type

**Values:**

**HARD** - Hard trigger. When this mode is set, the user has to manually press the trigger on the device after issuing the read call.

**SOFT_ONCE** - Soft trigger is used only once for a pending read or for the next issued read. When this mode is set, the scan beam will come up automatically without having to press the trigger on the device after issuing the read call.

**SOFT_ALWAYS** - Soft trigger is used for all pending scans and for future reads issued. When this mode is set, the scan beam will come up automatically without having to press the trigger on the device.