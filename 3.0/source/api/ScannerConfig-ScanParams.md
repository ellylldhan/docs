#ScannerConfig.ScanParams

The ScanParams class provides access to scanning parameters that are available for all decoders. 

> NOTE: When calling enable() after disable(), all the latest configuration parameter values (Config.DecoderParams, Config.ScannerParams, Config.ReaderParams and Config.InterfaceParams) will be set automatically.

##Public Fields
###audioStreamType
The audio stream type refers to type of streaming on which the scan beep should be played. The decodeAudioFeedbackUri specified must be available for the audio streaming type specified.

**Example Usage:**

    :::java
    scanParams.audioStreamType = AudioStreamType.RINGER;

**Type:**

com.symbol.emdk.barcode.[ScannerConfig.AudioStreamType](ScannerConfig#ScannerConfig.AudioStreamType)

###codeIdType
A Code ID character identifies the code type of a scanned bar code. This is useful when the reader is decoding more than one code type. Select a code ID character to insert between the prefix and the decoded symbol. Use enum [ScannerConfig.CodeIdType](ScannerConfig#ScannerConfig.CodeIdType).

**Example Usage:**

    :::java
    scanParams.codeIdType = CODE_ID_TYPE.NONE;

**Type:**

com.symbol.emdk.barcode.[ScannerConfig.CodeIdType](ScannerConfig#ScannerConfig.CodeIdType)

###decodeAudioFeedbackUri
Select an audio tone to sound upon a good decode. The valid audio files from the RingTone manager can be used for audio feedback.

**Example Usage:**

    :::java
    scanParams.decodeAudioFeedbackURI = "system/media/audio/notifications/decode-short.wav";
    scanParams.decodeAudioFeedbackUri = "sdcard/sample-audio.wav";
    scanParams.decodeAudioFeedbackUri = "sdcard/sample-audio.ogg";
	scanParams.decodeAudioFeedbackUri = "/sdcard/sample-audio.wav";

> Note: To achieve no feedback (silent) upon a good decode, specify an empty string as below:

	scanParams.decodeAudioFeedbackURI = "";

**Type:**

java.lang.String

###decodeHapticFeedback
Enable the device to vibrate upon a good decode.

**Example Usage:**

    :::java
    scanParams.decodeHapticFeedback = true;

**Type:**

boolean

###decodeLEDFeedback
Decoding LED Notification.

**Example Usage:**

    :::java
    scanParams.decodeLEDFeedback = true;

**Type:**

boolean

###decodeLEDTime
Decode LED ON duration upon successful decode in milliseconds. This value can be from 0ms to 1000ms with a step of 25ms.

**Example Usage:**

    :::java
    scanParams.decodeLEDTime = 75;

**Type:**

int