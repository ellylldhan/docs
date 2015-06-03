#PaymentDevice

PaymentDevice class will represent and provides access to the physical
 payment device.



**Example Usage:**
	
	:::java	
	 	
	  PaymentDevice paymentDevice = paymentManager.getDevice(DeviceIdentifer.DEFAULT);
	  paymentDevice.addDataListener(this);
	  paymentDevice.enable();
	
	  paymentDevice.readCardData();
	
	
	 @Override
	   public void onData(PaymentData paymentData) {
	
	   final PaymentData data = paymentData;
	   StringBuilder responseString = new StringBuilder();
	
	   switch (data.getDataType()) {
	
	   	case ENABLE:
	     		if(data.getResult() == PaymentResults.SUCCESS) {
	     			responseString.append("\nPayment device enable status: " + data.getResult().getDescription());
	    		 }
	   }
	  }
	
	  paymentDevice.disable();


##Public Methods

### isEnabled

**public boolean isEnabled()**



**Returns:**

boolean

### getDeviceInfo

**public DeviceInfo getDeviceInfo()**

Returns information about the payment device.

**Returns:**

com.symbol.emdk.payment.DeviceInfo

### enable

**public void enable()**

This is an asynchronous call and status of the enable method will be returned through the registered {@link PaymentDevice.DataListener}.
 This method is used to establish communication with the payment device and enable the payment device to do transactions.
 This method does not do any transactions.

 The following requirements must satisfy before calling enable method:
  - The payment device must paired with the mobile device.
  - The paired payment device name or MAC address must be set using {@link PaymentDevice.setInterfaceConfig(InterfaceConfig interfaceConfig)}.
  - The clients must implement {@link PaymentDevice.DataListener} and call {@link PaymentDevice.addDataListener(DataListener listener)}

  Only one session can be enabled at any given time.
  The Bluetooth connection will fail if the payment device is not already paired.
  The application can call other methods only after successful enabling.
  If the same of payment device is used by other application, enable will fail and returns error.
  You must call disable() when you are done the payment transactions,
  otherwise it will remain locked and be unavailable to other applications.

 

**Example Usage:**
	
	:::java	
	PaymentDevice paymentDevice = paymentManager.getDevice(DeviceIdentifer.DEFAULT);
	paymentDevice.addDataListener(this);
	paymentDevice.enable();
	
	
	


**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException

The exception will thrown if it fails enable the payment
             device.

             Possible Error codes: SUCCESS, AUTHORIZATION_FAILED, FAILURE,
             AUTHENTICATION_FAILED, ENABLE_FAILED, ALREADY_ENABLED,
             INVALID_CONFIGURATION, COMMUNICATION_ERROR, NO_DATA_LISTENER,
             DEVICE_IN_USE, CONNECTION_ERROR, DEVICE_NOT_PAIRED,
             INVALID_OBJECT, UNDEFINED

### disable

**public void disable()**

Disables the the payment device for transactions. This method closes the
 connection with the application and the payment device.

 

**Example Usage:**
	
	:::java	
	paymentDevice.disable();
	
	
	


**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException

The exception will thrown if any unexpected error occurs
             during the close call.

             Possible Error codes: SUCCESS, FAILURE, COMMUNICATION_ERROR,
             CONNECTION_ERROR, ALREADY_CLOSED, PREVIOUS_COMMAND_PENDING,
             DISABLE_FAILED, INVALID_OBJECT

### getConfig

**public PaymentConfig getConfig()**

Gets payment device configuration settings. On success the results will
 be stored on PaymentDevice.config.deviceConfig.
 Application must call this only after enabling the device.



**Example Usage:**
	
	:::java	
	try{
	PaymentConfig config = paymentDevice.getConfig();
	}catch (PaymentException e) {
	responseString.append(e.getResult().getDescription());
	}
	
	
	


**Returns:**

com.symbol.emdk.payment.PaymentConfig

**Throws:**

com.symbol.emdk.payment.PaymentException



### setConfig

**public void setConfig(PaymentConfig config)**

Sets payment device configuration settings. This method sets the modified
 values of PaymentDevice.config.deviceConfig fields. Application must call this only after enabling the device

  * 

**Example Usage:**
	
	:::java	
	try {
	PaymentConfig config = paymentDevice.getConfig();
	
	config.idleMessage = "Welcome";
	config.sleepModeTimeout =10000;
	config.getAllEncryptedData = false;
	config.dataEncryptionType = DataEncryptionType.NONE;
	paymentDevice.setConfig(config);
	}catch (PaymentException e) {
	responseString.append(e.getResult().getDescription());
	}
	
	
	


**Parameters:**

config

**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException



### enableKeypad

**public PaymentResults enableKeypad()**

This method enables the keypad on the payment device. The keypad must be explicitly
 enabled each time before calling the methods such as  readCardData() and promptPin(),
 which requires key entry input.Keyboard must remain enabled until disableKeypad  is
 called or the payment device goes to  lock screen mode.Enabling the keypad will enable
 keybeep  as well on the PD40-100 device. The payment device's keypad will be disabled
 either on default timeout or the parameter  sleepModeTimeout whichever is lower.

 

**Example Usage:**
	
	:::java	
	paymentDevice.enableKeypad();
	
	
	


**Returns:**

com.symbol.emdk.payment.PaymentResults

### enableKeypad

**public PaymentResults enableKeypad( timeOut)**

This method enables the keypad on the payment device. The keypad must be explicitly
 enabled each time before calling the methods such as  readCardData() and promptPin(),
 which requires key entry input.Keyboard must remain enabled until disableKeypad  is
 called or the payment device goes to  lock screen mode.Enabling the keypad will enable
 keybeep  as well on the PD40-100 device. The payment device's keypad will be disabled
 either on specified timeout or the parameter  sleepModeTimeout whichever is lower.

**Parameters:**

timeOut - The timeOut specifies how long the payment device's keypad should be in enabled state.
 The timeOut value unit is milliseconds.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 paymentDevice.enableKeypad(12000);
 }
 </pre>

 </blockquote>

**Returns:**

com.symbol.emdk.payment.PaymentResults

### disableKeypad

**public PaymentResults disableKeypad()**

Disables the keypad on the payment device.

 

**Example Usage:**
	
	:::java	
	paymentDevice.disableKeypad();
	
	
	


**Returns:**

com.symbol.emdk.payment.PaymentResults

### readCardData

**public PaymentResults readCardData( amount,  otherAmount, PaymentDevice.ReadMode readMode,  readTimeOut, ReadCardMessage readCardMessage)**

Reads the card data from the PAYMENT device. This is asynchronous call
 and card data is returned in the registered DataListener callback as
 described in the DataListener class. The character "|" not allowed in the
 message strings and it is used as special character in the EMDK for PD40-100 device.

**Parameters:**

amount - Amount for the transaction; this value is required to enable
            EMV contactless transactions. Allowed unto a maximum of 7
            digits.

otherAmount - For future use. Any additional amount information for the
            transaction; this value is used only used if EMV Contactless
            is supported. Allowed upto a maximum of 7 digits.

readMode - Card reading mode (swipe

readTimeOut - Read timeout in milliseconds. Application can set the timeout.
            But value must within threshold set by the payment device.

readCardMessage - The  ReadCardMessage class provides option configure the messages
            displayed on payment device while reading the card data on payment device
 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
  readCardMessage = new ReadCardMessage();
  readCardMessage.messageTitle ="MessageTitle";
  readCardMessage.screen1.message1 = "$2000.00";
  readCardMessage.screen1.message2 = "Transaction...";
 	paymentDevice.readCardData(1

**Returns:**

com.symbol.emdk.payment.PaymentResults

### readCardData

**public PaymentResults readCardData( amount,  otherAmount, PaymentDevice.ReadMode readMode,  readTimeOut)**

Reads the card data from the PAYMENT device. This is asynchronous call
 and card data is returned in the registered DataListener callback as
 described in the DataListener class.Results are captured by overriding
 OnData callback method.

**Parameters:**

amount - Amount for the transaction; this value is required to enable
            EMV contactless transactions. Allowed unto a maximum of 7
            digits.

otherAmount - For future use. Any additional amount information for the
            transaction; this value is used only used if EMV Contactless
            is supported. Allowed upto a maximum of 7 digits.

readMode - Card reading mode (swipe

readTimeOut - Read timeout in milliseconds. Application can set the timeout.
            But value must within threshold set by the payment device.
 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:

 	paymentDevice.readCardData(1

**Returns:**

com.symbol.emdk.payment.PaymentResults

### promptPin

**public PaymentResults promptPin( accountNumber,  minPinLength,  maxPinLength,  isPinOptional,  readTimeOut, PromptPinMessage promptPinMessage)**

Requests for a PIN and gets the encrypted PIN block. The encrypted data
 will be returned only if a debit key is injected into the payment device. This
 is asynchronous call and PIN data is returned in the registered
 DataListener callback as described in the DataListener class. Note: The
 character "|" not allowed in the message strings for PD40-100 payment device
 and it is used as special character in the in the EMDK for PD40-100 device. Requesting promptPin()
 continuously may pop up the timer on PD40-100 payment device for security
 reasons and application should wait for this before performing any other
 actions.

**Parameters:**

accountNumber - The account number or masked PAN used with the entered PIN to create the
            encrypted PIN Block (8 to 19 numeric digits).

minPinLength - Minimum PIN Length.

maxPinLength - Maximum PIN Length. A maximum length of up to 12 characters is
            allowed.

isPinOptional - If this flag is set True

readTimeOut - Read timeout in milliseconds. Application can set the timeout.
            But value must within threshold set by the payment device.

promptPinMessage - The PromptPinMessage class provides option configure the
            messages displayed on the payment device while reading the PIN.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
  promptPINMessage = new PromptPinMessage();
  promptPINMessage.messageTitle ="MessageTitle";
  promptPINMessage.screen1.message1 = Sale $1

**Returns:**

com.symbol.emdk.payment.PaymentResults

### promptPin

**public PaymentResults promptPin( accountNumber,  minPinLength,  maxPinLength,  isPinOptional,  readTimeOut)**

Requests for a PIN and gets the encrypted PIN block. The encrypted data
 will be returned only if a key is injected into the payment device. This
 is asynchronous call and PIN data is returned in the registered
 DataListener callback as described in the DataListener class. Requesting
 promptPin() continuously may pop up the timer on PD40-100 payment device for
 security reasons and application should wait for this before performing
 any other actions.

**Parameters:**

accountNumber - The account number or masked PAN used with the entered PIN to create the
            encrypted PIN Block (8 to 19 numeric digits).

minPinLength - Minimum PIN Length.

maxPinLength - Maximum PIN Length. A maximum length of up to 12 characters is
            allowed.

isPinOptional - If this flag is set True

readTimeOut - Read timeout in milliseconds. Application can set the timeout.
            But value must within threshold set by the payment device.

**Returns:**

com.symbol.emdk.payment.PaymentResults

### promptMenu

**public PaymentResults promptMenu( messageLine1,  messageLine2,  choice1,  choice2,  choice3,  choice4,  timeOut)**

Displays two lines of messages on the PAYMENT device and provides a menu
 with a maximum of 4 choices. This is asynchronous call and user selection
 is returned in the DataListener callback as described in the DataListener
 class. The character "|" not allowed in the message strings and it is
 used as special character in the EMDK for PD40-100.

**Parameters:**

messageLine1 - Message Line 1 to display on the PINPad screen. Maximum
            characters allowed for Choice + Message = 18 characters. For
            example

messageLine2 - Message Line 2 to display on the PINPad screen. Maximum
            characters allowed for Choice + Message = 18 characters. For
            example

choice1 - Choice text for selection from the PINPad using the function
            keys. Choice string can consist of up to 8 characters.

choice2 - Choice text for selection from the PINPad using the function
            keys. Choice string can consist of up to 8 characters.

choice3 - Choice text for selection from the PINPad using the function
            keys. Choice string can consist of up to 8 characters.

choice4 - Choice text for selection from the PINPad using the function
            keys. Choice string can consist of up to 8 characters.

timeOut - Timeout in milliseconds. Application can set the timeout. But
            value must within threshold set by the payment device.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 paymentDevice.promptMenu("messageLine1"

**Returns:**

com.symbol.emdk.payment.PaymentResults

### promptAdditionalInfo

**public PaymentResults promptAdditionalInfo( amount,  langCode,  promptForTip,  cashBack,  surcharge,  timeOut)**

Requests the user to confirm the amount and surcharge passed by the
 application and prompts the user to provide tip and cashback. The tip,
 cashback values and the confirmation if surcharge was accepted, will be
 returned to the application via the DataListener callback. If the user
 presses CORR or CANCEL keys, or the call times out, the corresponding
 error is returned. This is asynchronous call and data is returned in the
 DataListener callback as described in the DataListener class.

**Parameters:**

amount - Transaction amount value that is to be displayed.

langCode - Numeric value denoting the language code for determining the
            displayed language of the pre-defined prompt.

promptForTip - Indicates whether or not to prompt for tip and return the
            amount entered.

cashBack - Indicates whether or not to prompt for cashback and return the
            amount selected. The user would select the cashback amount
            from 4 pre-defined choices - $20

surcharge - An optional surcharge amount that is to be displayed and
            confirmed. A zero amount
            will cause this prompt to be bypassed

timeOut - Read timeout. Application can set the timeout. But value must
            within threshold set by the payment device.
 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 paymentDevice.promptAdditionalInfo(1.25

**Returns:**

com.symbol.emdk.payment.PaymentResults

### promptMessage

**public PaymentResults promptMessage( messageLine1,  messageLine2,  messageLine3,  messageLine4,  getUserConfirmation,  timeOut)**

Displays a maximum of 4 lines of messages on the payment device. This
 method also allows getting user confirmation. If the getUseConfirmation
 is set to false, this method works as synchronous else it is asynchronous
 method. The response will be returned via callback for asynchronous case.
 The character "|" not allowed in the message strings and it is used as
 special character in the EMDK for PD40-100 device.

**Parameters:**

messageLine1 - A message to display on line 1 of the PINPad screen. May
            consist of up to 16 characters

messageLine2 - A message to display on line 2 of the PINPad screen. May
            consist of up to 16 characters

messageLine3 - A message to display on line 2 of the PINPad screen. May
            consist of up to 16 characters

messageLine4 - A message to display on line 4 of the PINPad screen. May
            consist of up to 16 characters

getUserConfirmation - True or False. Allows the user to press OK (Enter key)

timeOut - Read timeout. Application can set the timeout. But value must
            within threshold set by the payment device.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 paymentDevice.promptMessage("messageLine1"

**Returns:**

com.symbol.emdk.payment.PaymentResults

### abort

**public PaymentResults abort()**

Abort or cancel previously issued request to device and display welcome
 screen on payment device. The payment device returns to idle state after
 the abort call.The abort method can abort the previous requests such as
 promptMessage with userCOnfirmation=true, promptMenu, readCardData,
 readCardData with message and promptAdditionalInfo.For the other requests,
 the abort method will return error as CANNOT_ABORT.

 

**Example Usage:**
	
	:::java	
	paymentDevice.abort();
	
	
	


**Returns:**

com.symbol.emdk.payment.PaymentResults

### getBatteryLevel

**public BatteryData getBatteryLevel()**

Query the battery level of the payment device.

  The possible battery levels returned by PD40 are
  0 Battery is almost 0%, the device needs to be charged before using"
	1 The battery icon display 1 grid, battery is between 1%-25%
  2 The battery icon display 2 grids, battery is between  25% - 50%
  3 The battery icon display 3 grids,battery is between  50%-75%
  4 The battery icon display 4 grids,battery is between  75%-100%

 

**Example Usage:**
	
	:::java	
	BatteryData data = paymentDevice.getBatteryLevel();
	String batteryLevel = String.valueOf(data.getValue());
	
	
	


**Returns:**

com.symbol.emdk.payment.BatteryData

### createMac

**public MacData createMac( u8MacData)**

This is a required transaction for Canada. Accepts a String of data to be
 MACed using the ANSI x9.91 standard and the MAC Working Key. This is
 used for MACing credit transactions when the PINPad is configured to
 support both credit and debit. This is synchronous call

**Parameters:**

u8MacData - String of data to be MACed. The length of the key should be
            16/32/48 bytes in HEX format.
 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 MacData data = paymentDevice.createMac("1112131415161718");
 }
 </pre>

 </blockquote>

**Returns:**

com.symbol.emdk.payment.MacData

### validateMac

**public PaymentResults validateMac( u8MacBlock,  langCode,  u8TpkKey,  u8TakKey,  message1,  message2,  u8MacData)**

Validates the response MAC and displays any authorization messages
 returned by the host. This method is made Asynchronous call because it is
 taking more processing time and response will be returned via registered
 data listener.

**Parameters:**

u8MacBlock - u8-character MAC Block to verify

langCode - Numeric value denoting the language code for determining the
            displayed language of the card entry prompts.

u8TpkKey - PIN (TPK) Key

u8TakKey - MAC (TAK) Key

message1 - Message Line 1 (0-16 bytes)

message2 - Message Line 2 (0-16 bytes)

u8MacData - Buffer to hold all data to be MACed
 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 paymentDevice.validateMac("u8MacBlock"

**Returns:**

com.symbol.emdk.payment.PaymentResults

### completeOnlineEmv

**public PaymentResults completeOnlineEmv(PaymentDevice.HostDecision hostDecision,  displayResult,  tagData)**

Completes an online EMV transaction for PIN management. The application
 must call authorizeCard before calling this API else API returns API_SEQUENCE_ERROR.
 This is an asynchronous call. After the processing, the response (i.e.,EmvData object)
 is returned through the registered DataListener.

**Parameters:**

hostDecision - HostDecision enum value which is the decision indicator from
            the host response.

displayResult - Indicator to note whether or not to display the final response
            message. The valid values are: false  Do not display

tagData - List of EMV data which contains EMV tag and its values.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 ArrayList<TagData> emvDataList = new ArrayList<TagData>();
 emvDataList.add(new TagData("5A085413330089601075"));
 paymentDevice.completeOnlineEmv(HostDecision.HOST_AUTHORIZED

**Returns:**

com.symbol.emdk.payment.PaymentResults

### getEmvTags

**public PaymentResults getEmvTags( emvTags)**

Gets tag information from the inserted card.
 This is an asynchronous call. The caller can request in  specific tags
 if the tag is not listed in the getEMVTags table.For more information on
 the table refer PaymentAPI_ProgrammersGuide. After the processing,
 the response (TagData contains TLV raw data as per EMV specification)
 and also its parsed tag,length and value format is returned through
 the registered DataListener. If we pass null as a parameter the API
 returns all the tag data listed in table in TLV format.
 The application must call  readCardData before calling the getEmvTags.

**Parameters:**

emvTags

**Returns:**

com.symbol.emdk.payment.PaymentResults

### setEmvTags

**public PaymentResults setEmvTags( emvTagData)**

Sets tag information for the inserted card. Valid EMV tag IDs and tag
 values should be passed. Passing invalid EMV tag IDs or tag values may
 cause the payment device to go into unstable state or unknown behavior.
 The payment device has to be rebooted in order to continue normal
 operation.

**Parameters:**

emvTagData - List of emv tag ID and its values be set on the inserted card.


 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
			  ArrayList<TagData> emvTagData = new ArrayList<TagData>();
            TagData data = new TagData("5A085413330089601075");
            emvTagData.add(data);
            paymentDevice.setEmvTags(emvTagData);
 }
 </pre>

 </blockquote>

**Returns:**

com.symbol.emdk.payment.PaymentResults

### authorizeCard

**public PaymentResults authorizeCard( amount,  otherAmount, PaymentDevice.MerchantDecision merchatDecision,  tags,  displayResult,  pinTryExceedStatus,  displayAmount,  displayAppExpired,  timeOut)**

Authorizes the EMV transaction amounts using the inserted chip (EMV)
 card. This is an asynchronous call. After processing, the authorize
 card response (AuthorizeCardData) is returned through the registered DataListener.
 Results are captured by overriding   OnData callback method.
 The application must call  readCardData before calling the AuthorizeCardData
 else API returns API_SEQUENCE_ERROR.For Online transactions PIN and KSN both
 be returned ,however offline transactions will not have KSN and PIN in the response data.

**Parameters:**

amount - Transaction amount value.

otherAmount - Other transaction amount value.

merchatDecision - The merchant decision notes additional handling for the EMV
            request based on required processor handling.

tags - is an list of EMV tags that is required at this transaction
            stage to be retrieved.

displayResult - True or False. True= display result on Payment device display.

pinTryExceedStatus

displayAmount - True or False. True= displays amount on Payment device display

displayAppExpired

timeOut

**Returns:**

com.symbol.emdk.payment.PaymentResults

### getLowBatteryThreshold

**public BatteryData getLowBatteryThreshold()**

Gets the acceptable low battery level. If the battery drops below this
 value, the device will not execute any of the selected commands.

 

**Example Usage:**
	
	:::java	
	BatteryData data = paymentDevice.getLowBatteryThreshold();
	String batteryLevel = String.valueOf(data.getValue());
	
	
	


**Returns:**

com.symbol.emdk.payment.BatteryData

### setLowBatteryThreshold

**public PaymentResults setLowBatteryThreshold( lowThreshold,  lowBatterMessage)**

Sets the acceptable low battery level. If the battery drops below this
 value, the device will not execute some of the selected payment
 transaction commands and it will return the error code indicating the
 battery is low.

**Parameters:**

lowThreshold - Below this value

lowBatterMessage - The message to be displayed when the battery level goes below
            the low threshold.

 Note :The battery check will be done only for the following commands:
		1.	ReadCardData
		2.	promptPin
		3.	completeOnlineEmv
		4.	createMac
		5.	validateMac
		6.	getEmvTags
		7.	setEmvTags
		8.	authorizeCard
 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 paymentDevice.setLowBatteryThreshold(2

**Returns:**

com.symbol.emdk.payment.PaymentResults

### getInterfaceConfig

**public InterfaceConfig getInterfaceConfig()**

This method provides access to get the interface configurations object.
 The field in the interface configuration must be updated and must call the setInterfaceConfig method to set these values.

**Returns:**

com.symbol.emdk.payment.InterfaceConfig

**Throws:**

com.symbol.emdk.payment.PaymentException

will be thrown if any error occurs.

         Possible Error codes: SUCCESS, FAILURE, UNDEFINED.

### setInterfaceConfig

**public void setInterfaceConfig(InterfaceConfig interfaceConfig)**

This method provides access to set the interface configurations like connect to the payment device. This
 must be set before calling the enable method. Setting the MAC address of payment device gives quicker
 response from enable method compared to setting the device name.
 This is an optional method to modify device information required to enable the payment device.
 

**Example Usage:**
	
	:::java	
	InterfaceConfig interfaceConfig = paymentDevice.getInterfaceConfig();
	interfaceConfig.macAddress = "8CDE520FE2FE";
	paymentDevice.setInterfaceConfig(interfaceConfig);
	payment.enable();
	
	
	


**Parameters:**

interfaceConfig - The Parameters to use for this payment device configurations.

**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException

will be thrown if any error occurs.

 		   Possible Error codes: SUCCESS, FAILURE, UNDEFINED.

### removeCard

**public void removeCard( message1,  message2)**

Instruct the user to remove the EMV card inserted in the payment device. This is an asynchronous call.
 This call prompts the user to remove the inserted EMV chip card and also clears the EMV data saved by readCardData method.
 This call  will not return until you remove the card.

**Parameters:**

message1 - The message which gives the information of type of card.

message2 - the message which gives instructions to user for the removal of the card.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 	paymentDevice.removeCard("EMVCard"

**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException

will be thrown if any error occurs.

### downloadFile

**public PaymentResults downloadFile(PaymentDevice.DownloadType downloadType,  filePath)**

downloadFile is an asynchronous call. The method allows the application to download the file such as EMV Params file,
 payment device firmware.The result status will be returned through the registered callback.Any other payment API call
 cannot  disturb downloading file , if done PREVIOUS_COMMAND_PENDING is returned.

**Parameters:**

downloadType - This indicates the type of File to download either DownloadType.EMVPARA or DownloadType.FIRMARE  file.

filePath - This is  file location accepted for downloading files.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:
 	paymentDevice.downloadFile(DownloadType.EMVPARAM

**Returns:**

com.symbol.emdk.payment.PaymentResults

### downloadFile

**public PaymentResults downloadFile(PaymentDevice.DownloadType downloadType,  fileData)**

downloadFile is an asynchronous call. The application must be able to download or update the file such as EMV parameter,Firmware file or font file to the payment Device.
 The  downloadFile status will be returned through the registered callback.Once application starts download, other requests are not allowed and the PREVIOUS_COMMAND_PENDING
 will be returned until download completes.

**Parameters:**

downloadType - The type of File to download such as  EMV parameter 

fileData - The  complete download data.The partial data is not allowed.

 <p>
 <blockquote>

 <pre>
 {@code
 Example Usage:




 in = new FileInputStream("//sdcard//Payment//EmvParam");
 int bufferSize = in.available();
 byte[] emvParamBuffer = new byte[bufferSize];

 while ((byteread = in.read(emvParamBuffer)) != -1) {
	result = paymentDevice.downloadFile(DownloadType.EMVPARA

**Returns:**

com.symbol.emdk.payment.PaymentResults

### addDataListener

**public void addDataListener(PaymentDevice.DataListener listener)**

The client application can register to get data notification via callbacks.

**Parameters:**

listener - The DataListener callabck object.

**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException

Exception will be thrown if any error occurs during this
             call.

### removeDataListener

**public void removeDataListener(PaymentDevice.DataListener listener)**

The client application can un-register to get data notification via callbacks.

**Parameters:**

listener

**Returns:**

void

**Throws:**

com.symbol.emdk.payment.PaymentException

Exception will be thrown if any error occurs during this call.

##Public Enums

###PaymentDevice.ReadMode

Lists type of read mode supported by the readCardData.

**Values:**

* **SWIPE**

* **INSERT**

* **TOUCH**

* **MANUAL**

* **ALL**

###PaymentDevice.DataEncryptionType

Lists the type pf Encryption Algorithms applied on the data.

**Values:**

* **NONE**

* **TRIPLE_DES**

* **AES**

* **RSA_1024**

* **RSA_2048**

###PaymentDevice.CardEncodeType

List indicates the type of encoding that was found on the card.

**Values:**

* **ISO_ABA**

* **NON_ISO_ABA**

###PaymentDevice.DownloadType

The payment Device download or update type.

**Values:**

* **FIRMWARE**

* **EMVPARAM**

###PaymentDevice.HostDecision

Decision indicator from the host response.

**Values:**

* **HOST_AUTHORIZED**

* **HOST_DECLINE**

* **CONNECT_FAILED**

###PaymentDevice.MerchantDecision

The merchant decision notes additional handling for the EMV request based
 on required processor handling.

**Values:**

* **REQUEST_TC**

* **FORCE_ONLINE**

* **FORCE_DECLINE**
