#EMDK For Android API List

## Core and ProfileManager APIs
The following APIs are to be used to process EMDK features and profiles using the [Profile Manager](../guide/profiles/usingwizard) as well as getting information about the EMDK.

###EMDKBase
* [EMDKBase](../api/EMDKBase)

###EMDKManager
* [EMDKManager](../api/EMDKManager) 
* [EMDKManager.EMDKListener](../api/EMDKManager-EMDKListener) 

###EMDKResults
* [EMDKResults](../api/EMDKResults) 

###ProfileConfig
* [ProfileConfig](../api/ProfileConfig)
* [ProfileConfig.ActivitySelection](../api/ProfileConfig-ActivitySelection) 
* [ProfileConfig.ActivitySelection.ActivityElement](../api/ProfileConfig-ActivitySelection-ActivityElement) 
* [ProfileConfig.DataCapture](../api/ProfileConfig-DataCapture) 
* [ProfileConfig.DataCapture.Barcode](../api/ProfileConfig-DataCapture-Barcode) 
* [ProfileConfig.DataCapture.Barcode.Decoders](../api/ProfileConfig-DataCapture-Barcode-Decoders) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams](../api/ProfileConfig-DataCapture-Barcode-DecoderParams) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Codabar](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Codabar) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Code11](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Code11) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Code128](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Code128) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Code39](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Code39) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Code93](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Code93) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Composite_AB](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Composite_AB)
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Discrete_2of5](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Discrete_2of5)
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Interleaved_2of5](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Interleaved_2of5) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.Matrix_2of5](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-Matrix_2of5) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.MSI](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-MSI) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.UK_Postal](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-UK_Postal) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.UPCA](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-UPCA) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.UPCE0](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-UPCE0) 
* [ProfileConfig.DataCapture.Barcode.DecoderParams.UPCE1](../api/ProfileConfig-DataCapture-Barcode-DecoderParams-UPCE1) 
* [ProfileConfig.DataCapture.Barcode.ReaderParams](../api/ProfileConfig-DataCapture-Barcode-ReaderParams) 
* [ProfileConfig.DataCapture.Barcode.ScanParams](../api/ProfileConfig-DataCapture-Barcode-ScanParams) 
* [ProfileConfig.DataCapture.Barcode.UpcEanParams](../api/ProfileConfig-DataCapture-Barcode-UpcEanParams) 
* [ProfileConfig.DataCapture.MSR](../api/ProfileConfig-DataCapture-MSR) 
* [ProfileConfig.DataCapture.DataDelivery](../api/ProfileConfig-DataCapture-DataDelivery) 
* [ProfileConfig.DataCapture.DataDelivery.BasicDataFormatting](../api/ProfileConfig-DataCapture-DataDelivery-BasicDataFormatting) 
* [ProfileConfig.DataCapture.DataDelivery.Intent](../api/ProfileConfig-DataCapture-DataDelivery-Intent) 
* [ProfileConfig.DataCapture.DataDelivery.Keystroke](../api/ProfileConfig-DataCapture-DataDelivery-Keystroke)

###ProfileManager
* [ProfileManager](../api/ProfileManager) 

###VersionManager
* [VersionManager](../api/VersionManager) 



## Barcode APIs
The following APIs are used when you wish to handle all barcode scanning entirely in Java. These API's work independently of any [Data Capture profiles.](../guide/profiles/profilebarcode)

###BarcodeManager
* [BarcodeManager](../api/BarcodeManager)
* [BarcodeManager.ScannerConnectionListener](../api/BarcodeManager-ScannerConnectionListener)
* [BarcodeManager.ScannerConnectionListener.ConnectionStatus](../api/BarcodeManager-ScannerConnectionListener-ConnectionStatus)

###Collection
* [Collection.ScanData](../api/Collection-ScanData)

###ScanDataCollection
* [ScanDataCollection](../api/ScanDataCollection)


###Scanner
* [Scanner](../api/Scanner)
* [Scanner.DataListener](../api/Scanner-DataListener)
* [Scanner.StatusListener](../api/Scanner-StatusListener)

###ScannerConfig
* [ScannerConfig](../api/ScannerConfig)
* [ScannerConfig.DecoderParams](../api/ScannerConfig-DecoderParams)
* [ScannerConfig.DecoderParams.AustralianPostal](../api/ScannerConfig-DecoderParams-AustralianPostal)
* [ScannerConfig.DecoderParams.Aztec](../api/ScannerConfig-DecoderParams-Aztec)
* [ScannerConfig.DecoderParams.BaseDecoder](../api/ScannerConfig-DecoderParams-BaseDecoder)
* [ScannerConfig.DecoderParams.CanadianPostal](../api/ScannerConfig-DecoderParams-CanadianPostal)
* [ScannerConfig.DecoderParams.Chinese2of5](../api/ScannerConfig-DecoderParams-Chinese2of5)
* [ScannerConfig.DecoderParams.CodaBar](../api/ScannerConfig-DecoderParams-CodaBar)
* [ScannerConfig.DecoderParams.Code11](../api/ScannerConfig-DecoderParams-Code11)
* [ScannerConfig.DecoderParams.Code128](../api/ScannerConfig-DecoderParams-Code128)
* [ScannerConfig.DecoderParams.Code39](../api/ScannerConfig-DecoderParams-Code39)
* [ScannerConfig.DecoderParams.Code93](../api/ScannerConfig-DecoderParams-Code93)
* [ScannerConfig.DecoderParams.CompositeAB](../api/ScannerConfig-DecoderParams-CompositeAB)
* [ScannerConfig.DecoderParams.CompositeC](../api/ScannerConfig-DecoderParams-CompositeC)
* [ScannerConfig.DecoderParams.D2of5](../api/ScannerConfig-DecoderParams-D2of5)
* [ScannerConfig.DecoderParams.DataMatrix](../api/ScannerConfig-DecoderParams-DataMatrix)
* [ScannerConfig.DecoderParams.DutchPostal](../api/ScannerConfig-DecoderParams-DutchPostal)
* [ScannerConfig.DecoderParams.Ean13](../api/ScannerConfig-DecoderParams-Ean13)
* [ScannerConfig.DecoderParams.Ean8](../api/ScannerConfig-DecoderParams-Ean8)
* [ScannerConfig.DecoderParams.Gs1Databar](../api/ScannerConfig-DecoderParams-Gs1Databar)
* [ScannerConfig.DecoderParams.Gs1DatabarExp](../api/ScannerConfig-DecoderParams-Gs1DatabarExp)
* [ScannerConfig.DecoderParams.Gs1DatabarLim](../api/ScannerConfig-DecoderParams-Gs1DatabarLim)
* [ScannerConfig.DecoderParams.I2of5](../api/ScannerConfig-DecoderParams-I2of5)
* [ScannerConfig.DecoderParams.JapanesePostal](../api/ScannerConfig-DecoderParams-JapanesePostal)
* [ScannerConfig.DecoderParams.Korean3of5](../api/ScannerConfig-DecoderParams-Korean3of5)
* [ScannerConfig.DecoderParams.Matrix2of5](../api/ScannerConfig-DecoderParams-Matrix2of5)
* [ScannerConfig.DecoderParams.MaxiCode](../api/ScannerConfig-DecoderParams-MaxiCode)
* [ScannerConfig.DecoderParams.MicroPdf](../api/ScannerConfig-DecoderParams-MicroPdf)
* [ScannerConfig.DecoderParams.MicroQr](../api/ScannerConfig-DecoderParams-MicroQr)
* [ScannerConfig.DecoderParams.Msi](../api/ScannerConfig-DecoderParams-Msi)
* [ScannerConfig.DecoderParams.Pdf417](../api/ScannerConfig-DecoderParams-Pdf417)
* [ScannerConfig.DecoderParams.QrCode](../api/ScannerConfig-DecoderParams-QrCode)
* [ScannerConfig.DecoderParams.Signature](../api/ScannerConfig-DecoderParams-Signature)
* [ScannerConfig.DecoderParams.Tlc39](../api/ScannerConfig-DecoderParams-Tlc39)
* [ScannerConfig.DecoderParams.TriOptic39](../api/ScannerConfig-DecoderParams-TriOptic39)
* [ScannerConfig.DecoderParams.UkPostal](../api/ScannerConfig-DecoderParams-UkPostal)
* [ScannerConfig.DecoderParams.UpcEanParams](../api/ScannerConfig-DecoderParams-UpcEanParams)
* [ScannerConfig.DecoderParams.Upca](../api/ScannerConfig-DecoderParams-Upca)
* [ScannerConfig.DecoderParams.Upce0](../api/ScannerConfig-DecoderParams-Upce0)
* [ScannerConfig.DecoderParams.Upce1](../api/ScannerConfig-DecoderParams-Upce1)
* [ScannerConfig.DecoderParams.Us4State](../api/ScannerConfig-DecoderParams-Us4State)
* [ScannerConfig.DecoderParams.Us4StateFics](../api/ScannerConfig-DecoderParams-Us4StateFics)
* [ScannerConfig.DecoderParams.UsPlanet](../api/ScannerConfig-DecoderParams-UsPlanet)
* [ScannerConfig.DecoderParams.UsPostNet](../api/ScannerConfig-DecoderParams-UsPostNet)
* [ScannerConfig.DecoderParams.WebCode](../api/ScannerConfig-DecoderParams-WebCode)
* [ScannerConfig.ReaderParams](../api/ScannerConfig-ReaderParams)
* [ScannerConfig.ReaderParams.ReaderSpecific](../api/ScannerConfig-ReaderParams-ReaderSpecific)
* [ScannerConfig.ReaderParams.ReaderSpecific.CameraSpecific](../api/ScannerConfig-ReaderParams-ReaderSpecific-CameraSpecific)
* [ScannerConfig.ReaderParams.ReaderSpecific.ImagerSpecific](../api/ScannerConfig-ReaderParams-ReaderSpecific-ImagerSpecific)
* [ScannerConfig.ReaderParams.ReaderSpecific.LaserSpecific](../api/ScannerConfig-ReaderParams-ReaderSpecific-LaserSpecific)
* [ScannerConfig.ScanParams](../api/ScannerConfig-ScanParams)

###ScannerException
* [ScannerException](../api/ScannerException)

###ScannerInfo
* [ScannerInfo](../api/ScannerInfo)

###StatusData
* [StatusData](../api/StatusData)