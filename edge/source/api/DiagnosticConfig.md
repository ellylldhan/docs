#DiagnosticConfig

The diagnostic configuration class has to be configured before calling the get diagnostics parameter data.



##Constructors

**DiagnosticConfig**

DiagnosticsConfig Constructor

**Parameters:**

averageCurrent

in ma

int

tripInMinutes

in mins

int

##Public Fields

###averageCurrent

The average current consumption in mA. 
 When this is 0, the default value will be selected based on the running average.

**Type:**

int

###tripInMinutes

The shopping trip duration in minutes.
 When this is 0, the value will be generated for 45 minutes.

**Type:**

int
