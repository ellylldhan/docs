#ScannerConfig.ReaderParams.ReaderSpecific.LaserSpecific

LaserSpecific class provides access to the laser scanner specific parameters.

##Public Fields
###beamTimer
Sets the maximum amount of time that the reader remains on (0 - 60,000 ms in increments of 100 ms). A value of 0 sets the reader to stay on indefinitely. 

**Example Usage:**

    :::java
    readerParams.beamTimer = 1500;

**Type:**

int

###continuousRead
ContinuousRead class provides access to continuous scanning related parameters.

**Type:**

[ScannerConfig-ReaderParams-ReaderSpecific-ContinuousRead](ScannerConfig-ReaderParams-ReaderSpecific-ContinuousRead)


###linearSecurityLevel
Sets the number of times a bar code is read to confirm an accurate decode. Use enum [ScannerConfig.LinearSecurityLevel](ScannerConfig#ScannerConfig.LinearSecurityLevel).

**Example Usage:**

    :::java
    readerParams.linearSecurityLevel = LinearSecurityLevel.ALL_THRICE;

**Type:**

com.symbol.emdk.barcode.[ScannerConfig.LinearSecurityLevel](ScannerConfig#ScannerConfig.LinearSecurityLevel)

###inverse1DMode
This parameter allows the user to select decoding on inverse 1D bar codes. Use enum [ScannerConfig.Inverse1DMode](ScannerConfig#ScannerConfig.Inverse1DMode).

**Example Usage:**

    :::java
    readerParams.cameraSpecific.inverse_1d_mode = Inverse1DMode.AUTO;

**Type:**

com.symbol.emdk.barcode.[ScannerConfig.Inverse1DMode](ScannerConfig#ScannerConfig.Inverse1DMode)

###powerMode
Set scanner power mode. Use enum [ScannerConfig.PowerMode](ScannerConfig#ScannerConfig.PowerMode).

**Type:**

com.symbol.emdk.barcode.[ScannerConfig.PowerMode](ScannerConfig#ScannerConfig.PowerMode)