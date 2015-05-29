#ProfileConfig.DataCapture
Class for dealing with data capture profile data ProfileConfig.DataCapture

**Example Usage:**

	:::java
	DataCapture dataCapture = profileConfig.dataCapture;

**Version:**

2.0

##Public Fields

###barcode
Gets and Sets Barcode configuration object.

**Example Usage:**

	:::java
	profileConfig.dataCapture.barcode.decoders.code11 = ENABLED_STATE.DEFAULT;


**Type:**

com.symbol.emdk.[ProfileConfig.DataCapture.Barcode](ProfileConfig.DataCapture.Barcode)

###dataDelivery
Gets and Sets DataDelivery configuration object.

**Example Usage:**

	:::java
	profileConfig.dataCapture.dataDelivery.keystroke.ime_output_enabled = ENABLED_STATE.DEFAULT;


**Type:**

com.symbol.emdk.[ProfileConfig.DataCapture.DataDelivery](ProfileConfig.DataCapture.DataDelivery)

###msr
Gets and Sets MSR configuration object.

**Example Usage:**

	:::java
	profileConfig.msr.msr_input_enabled = ENABLED_STATE.DEFAULT;


**Type:**

com.symbol.emdk.[ProfileConfig.DataCapture.MSR](ProfileConfig.DataCapture.MSR)

