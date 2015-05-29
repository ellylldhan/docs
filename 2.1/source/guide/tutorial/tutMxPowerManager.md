# Power Management using Power Manager API

## Overview

This guide will walk you through creating an EMDK For Android application that will use Mx features introduced in EMDK V 2.1 API to perform device configurations. Mx represents a suite of Enterprise Features on top of standard, commercially available Android Open Source Project. So this tutorial will focus on [Power Manager](../guide/profiles/refPowerManager) API, which allows user to perform Power Management operations on Motorola Enterprise Android devices. Theses operations include setting the device in sleep mode, rebooting the device and updating device Operating System as follows:

**1. Sleep Mode:**

This feature allows device to enter the sleep mode in order to conserve power.

**2. Device Reboot:**

Device Reboot feature restarts the Motorola Enterprise Android device from the app itself.

**3. OS Update:**  

This Power Manager feature allows you to update the operating system of your Motorola Enterprise Android device. The user needs to provide path of update package (zip file) that resides in the device's external SD Card. Based on the package (zip file), the user can perform following operations using OS Update feature:

   > Note: Copy the update package to external SD Card in order to make update OS work. If you copy update package to the internal SD card of the device, the OS Update feature won't work.  

* **Enterprise Reset:** Resets the device data except Mx Enterprise Packages.
* **Factory Reset:** Resets the device data.
* **OS Upgrade:** Upgrades/Downgrades device's Operating System.
 
In this tutorial, We would be implementing all three features of Power Manager to understand how they work. 
 
###Prerequisites

* Java Development Kit (JDK)
* Android Developer Tools (ADT)
* Motorola EMDK for Android V 2.1 and above
* Download the respective OS update/Factory Reset/Enterprise Reset package (zip file) from [here](https://portal.motorolasolutions.com/Support/US-EN/Mobile+Networks+RFID+and+BarCode+Scanners/Mobile+Computers/Handheld+Computers/TC55) and copy that file to external SD card of the device.

    > Note: This above link provides the Update Packages of Motorola TC55 device only, which we have used in this tutorial. If you are using some other Motorola Enterprise Android device then download the respective update package from [here](https://portal.motorolasolutions.com/Support/US-EN/Mobile+Networks+RFID+and+BarCode+Scanners/Mobile+Computers/Handheld+Computers)

For more information about setting up the EMDK please see the EMDK Overview.

## Creating The Project
1.  Create new Android Application project.
  
    ![img](images/MxPowerManagerTutorialImages/create_new_app.jpg)

2.  Assign names for the application and package.
 
3.  Set the minimum required SDK to "API 16: Android 4.1 (Jelly Bean)".
  
    ![img](images/MxPowerManagerTutorialImages/set_app_name.jpg)

4.  Click "Next".
  
    ![img](images/MxPowerManagerTutorialImages/configure_project.jpg)
  
5.  Click "Next".
  
    ![img](images/MxPowerManagerTutorialImages/configure_launcher_icon.jpg)
  
6.  Click "Next".  

7.  Select "Empty Activity" Click "Next".  

    ![img](images/MxPowerManagerTutorialImages/create_activity.jpg)  

    >Note:  
    >If "Empty Activity" is not available make sure you are using "Android SDK Tools 22.6.3" and "Android SDK Platform Tools 19.0.2"

7.  Click "Next".  

    ![img](images/MxPowerManagerTutorialImages/empty_activity.jpg)
  
8.  Click "Finish".

    >Note:  
    >Currently there is nothing under "\assets" folder.  
    
    ![img](images/MxPowerManagerTutorialImages/main_activity.jpg)  

## Enabling the EMDK
1. Select the project.
  
2. Select "File -> Properties" or right click on the project and select "Properties".
  
    ![img](images/MxPowerManagerTutorialImages/project_properties_button_1.jpg)
   
    ![img](images/MxPowerManagerTutorialImages/project_properties_button_2.jpg)
   
3. Click "Android" from the left pane.
  
    ![img](images/MxPowerManagerTutorialImages/project_properties.jpg)
 
4. Select "EMDK APIs 2.1" from the list of Project Build Targets.
  
    ![img](images/MxPowerManagerTutorialImages/project_properties_build_target.jpg)  

    >Note:  
    >If "EMDK APIs 2.1" is not on the list of Build Targets, please confirm you have installed Android API 16 SDK Platform.

5. Click "Apply" and "OK".  
    >Note:  
    >The EMDK library will be added to the project.  
    
    ![img](images/MxPowerManagerTutorialImages/emdk_library_added.jpg) 

    >Note:
    >If you are using Java 1.7 as the compiler, you may see this error
    
    ![img](images/MxPowerManagerTutorialImages/compiler_error.jpg) 

    > To correct this, you will need to change the compiler to use 1.6
    
    > * Click on the Java Compiler
    > * Click Enable project specific settings
    > * Select 1.6 for Compiler compliance level
    
    ![img](images/MxPowerManagerTutorialImages/java_compiler_settings.jpg) 

## Adding The Power Manager Profile Feature
1. Select "MxPowerManagerTutorial" project from Package Explorer.
    
2. Click "EMDK" menu and select "Profile Manager".
  
    ![img](images/MxPowerManagerTutorialImages/profile_manager_button.jpg)
  
3. The EMDK Profile Manager Window will appear.
  
    ![img](images/MxPowerManagerTutorialImages/emdk_profile_manager.jpg)
  
4. Click "Create" and assign a name for the profile (Ex: PowerManagerProfile).
  
    ![img](images/MxPowerManagerTutorialImages/create_new_profile.jpg)
  
5. Click "Create". The Profile Editor window will appear.
  
    ![img](images/MxPowerManagerTutorialImages/profile_editor.jpg)
  
6. Select the "Power Manager" feature from the list and click "Right Arrow". Using this feature you can perform various Power Management operations through your apps on the Motorola enterprise Android device. These operations include setting the device into sleep mode , rebooting the device and updating OS of the Motorola Enterprise Android devices as explained earlier.

    > Note: This profile editor of EMDK V 2.1 has some new features compared to previous EMDK V 2.0

The earlier features are categorized on the basis of their functionality. (For Example - Data Input can be done in two ways viz Barcode and MSR). The new features introduced in EMDK V 2.1 are MX (Mobility Extension) interfaces that are used to configure the Motorola enterprise Android devices based on requirements.      
 
 
7. Click on the Power Manager feature. The parameter list will be populated.  
  
    ![img](images/MxPowerManagerTutorialImages/select_power_manager_feature.jpg)

8. Now Click on the drop-down of the action field to see the supported features by Power Manager.

    ![img](images/MxPowerManagerTutorialImages/power_manager_features.jpg)

    There are four features shown in the drop down, three of which have been explained earlier. As the name suggests, forth feature `Do Nothing` does nothing. We would be configuring above mentioned three features from the application itself. Hence let us select the `Reset Action` in the wizard as `Do Nothing`.

    > Note: You could select any option you want in the wizard and the application will implement that feature on the launch.

    ![img](images/MxPowerManagerTutorialImages/feature_do_nothing.jpg)

    > Note: Provide some name in the Name field (Ex. MyPowerManager) in order to refer that specific feature of Profile.
    > You can also keep Name field empty.
  
9.  Click Apply and Finish. 

    ![img](images/MxPowerManagerTutorialImages/power_manager_profile_created.jpg)  

10. Click "Close".   

    >Note:  
    >Now the "EMDKConfig.xml" is created under "\assets" folder. This file will contain a definition of all of your profiles that you create. 
    
    ![img](images/MxPowerManagerTutorialImages/emdk_config_file.jpg)
  
12. You can inspect the EMDKConfig.xml to see it is reflecting the changes made to the parameters via EMDK Profile Manager GUI earlier.  However, it is advised that this file not be manually updated and only be controlled via the Profile Manager. So you can see the entry of the 'Reset Action' parameter of Power Manager feature and the value assigned to it is 0.

    Now there are specific values that are assigned to the parameters in Power Manager feature:

    * 0 - Do Nothing
    * 1 - Sleep Mode
    * 4 - Reboot
    * 8 - OS Update

    Based on user selection, these values would be assigned against these parameters of the Power Manager feature in EMDKConfig file.

    > Note: These values are useful when we modify Profile from the application using EMDK API, which we will see shortly in this tutorial.

    ![img](images/MxPowerManagerTutorialImages/emdk_config_file_entries.jpg)    

## Enabling Android Permissions
1. Modify the Application's Manifest.xml to use the EMDK library and to set permission for the EMDK.
  
    ![img](images/MxPowerManagerTutorialImages/manifest_file.jpg)

    You must first enable permissions for 'com.symbol.emdk.permission.EMDK':  
   
        :::xml
        <uses-permission android:name="com.symbol.emdk.permission.EMDK"/> 

    Then you must enable the library:  
      
        :::xml
        <uses-library android:name="com.symbol.emdk"/>

    When done, your manifest.xml should look like:

    ![img](images/MxPowerManagerTutorialImages/manifest_permissions_added.jpg) 

##Adding Some Code    
1. Now we will start to add some code. 

    First you must add references to the libraries:  
    
        :::java
        import com.symbol.emdk.*;  
        import com.symbol.emdk.EMDKManager.EMDKListener;  
		import android.widget.Toast;    

    Then you must extend the activity to implement EMDKListener. Use Eclipse’s Content Assist to implement the unimplemented functions of `onOpened` and `onClosed`.    
    
        :::java
        public class MainActivity extends Activity implements EMDKListener {  
          
            .. .. .. .. .. .. ...  
          
            @Override  
            public void onClosed() {  
                   // TODO Auto-generated method stub  
            }  
          
            @Override  
            public void onOpened(EMDKManager emdkManager) {  
                   // TODO Auto-generated method stub  
            }  
          
        }      

    We will now create some global variables to hold the profile name as well as instance objects of EMDKManager and ProfileManager. We will also create global variables to hold the UI elements and values that are required in this application. These variables would be used throughout the code. 

    >Note:
    >Verify the Profile name in the code with the one created in the Profile Manager. They both should be identical.    
    
        :::java
        // Assign the profile name used in EMDKConfig.xml
	    private String profileName = "PowerManagerProfile";

	    // Declare a variable to store ProfileManager object
	    private ProfileManager profileManager = null;

	    // Declare a variable to store EMDKManager object
	    private EMDKManager emdkManager = null;

	    // Text View for displaying status of EMDK operations
	    private TextView statusTextView = null;

	    // Radio Group to hold Radio Buttons for Power Manager Options
	    private RadioGroup pwrRadioGroup = null;

	    // Edit Text that allows user to enter the path of the update package from
	    // external SD Card
	    private EditText zipFilePathEditText;

	    // String that gets the path of the OS Update Package from Edit Text
	    private String zipFilePath;

	    // Initial Value of the Power Manager options to be executed in the
	    // onOpened() method when the EMDK is ready. Default Value set in the wizard
	    // is 0.
	    // 0 -> Do Nothing
	    // 1 -> Sleep Mode
	    // 4 -> Reboot
	    // 8 -> OS Update
	    private int value = 0;

	    // String that contains status of the Power Manager operations that are
	    // executed based on user selected features
	    private String resultString = "";

    So the code looks like:

    ![img](images/MxPowerManagerTutorialImages/global_variable_entry.jpg)

    In the onCreate method, we call getEMDKManager so that the EMDK can be initialized and checked to see if it is ready. 

        :::java
        //The EMDKManager object will be created and returned in the callback.  
        EMDKResults results = EMDKManager.getEMDKManager(getApplicationContext(), this);  
          
        //Check the return status of getEMDKManager  
		if (results.statusCode == EMDKResults.STATUS_CODE.SUCCESS) {

			// EMDKManager object creation success

		} else {

			// EMDKManager object creation failed

		}


    So far your code should look like:
     
     ![img](images/MxPowerManagerTutorialImages/on_create_added.jpg) 

2. Now we need to use the `onOpened` method to get a reference to the EMDKManager. The EMDKListener interface will trigger this event when the EMDK is ready to be used. Hence we will update the status in the `statusTextView`. The EMDKListener interface must be implemented in order to get a reference to the EMDKManager APIs. This event will pass the EMDKManager instance and we assign it to the global variable `emdkManager` that we created in the previous steps. We then use that instance object to get an instance of ProfileManager and assign it to the global variable `profileManager`. This is how we will interface with the APIs in the rest of the code:

    > Note: 
    > Rename the argument of `onOpened` method from `arg0` to `emdkManager`  

        :::java
        // This callback will be issued when the EMDK is ready to use.
		statusTextView.setText("EMDK open success.");

		this.emdkManager = emdkManager;

		// Get the ProfileManager object to process the profiles
		profileManager = (ProfileManager) emdkManager
				.getInstance(EMDKManager.FEATURE_TYPE.PROFILE);         
    
    Now that we have a reference to ProfleManager, we use it to install and activate the profile we built earlier using the `processProfile` method. We could have also performed this action at a different time, say when someone pressed a button, but we chose to do it as soon as the EMDK was ready:  

        :::java
        if (profileManager != null) {
			String[] modifyData = new String[1];
			// Call processPrfoile with profile name and SET flag to create the
			// profile. The modifyData can be null.

			EMDKResults results = profileManager.processProfile(profileName,
					ProfileManager.PROFILE_FLAG.SET, modifyData);

			if (results.statusCode == EMDKResults.STATUS_CODE.SUCCESS) {
				resultString = "Profile update success.";
			} else {
				resultString = "Profile update failed.";
			}

			statusTextView.setText(resultString);
		}  

    Your complete onOpened method should now look like this:
    
    ![img](images/MxPowerManagerTutorialImages/on_opened_method.jpg)  
    
3. Now let's override the "onDestroy" method so we can release the EMDKManager resources:  

        :::java
        @Override  
        protected void onDestroy() {  
            // TODO Auto-generated method stub  
            super.onDestroy();  
            //Clean up the objects created by EMDK manager  
            emdkManager.release();  
        } 

    Your onDestroy method should now look like this:  

    ![img](images/MxPowerManagerTutorialImages/on_destroy_method.jpg) 

4. Let us set the required layout/View for this tutorial. Remove all the code, inside "res/layout/activity_main.xml".

5. Add the following code that has three radio buttons that enable user to select a specific Power Manager feature, an Edit Text that allows user to enter the external SD Card path to the OS update package (zip file), a Text View that displays the status of every operation the user performs and a Button that triggers the user selected Power Manager feature and configures the device based on that.

    > Note: Copy the update package to external SD Card in order to make update OS work. If you copy update package to the internal SD card of the device, the OS Update feature won't work.  

        :::xml
        <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_margin="20dip"
        tools:context=".MainActivity" >

          <LinearLayout
          android:id="@+id/linearLayout1"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_alignParentLeft="true"
          android:layout_alignParentRight="true"
          android:layout_alignParentTop="true"
          android:orientation="vertical" >
          </LinearLayout>

          <TextView
          android:id="@+id/textView1"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_alignLeft="@+id/linearLayout1"
          android:layout_alignRight="@+id/linearLayout1"
          android:layout_below="@+id/buttonSet"
          android:layout_marginTop="20dp"
          android:text="Status:" />

          <RadioGroup
          android:id="@+id/radioGroupPwr"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_alignLeft="@+id/linearLayout1"
          android:layout_alignTop="@+id/linearLayout1" >

          <TextView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_margin="10dip"
          android:text="Choose your Power Manager Option:"
          android:textSize="16sp"
          android:textStyle="bold" />

          <RadioButton
          android:id="@+id/radioSuspend"
          android:layout_width="279dp"
          android:layout_height="wrap_content"
          android:text="Suspend (sleep mode)" />

          <RadioButton
          android:id="@+id/radioReset"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:text="Perform reset (reboot)" />

          <RadioButton
          android:id="@+id/radioOSUpdate"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:text="Perform OS Update" />

          <TextView
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_margin="10dip"
          android:text="Specify Path and Name of the Zip file in the file system for OS Update"
          android:textSize="16sp" />

          <EditText
          android:id="@+id/et_zip_file_path"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:hint="Path and Name of Zip file"
          android:maxLines="2" />
          </RadioGroup>

          <Button
          android:id="@+id/buttonSet"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@+id/radioGroupPwr"
          android:layout_centerHorizontal="true"
          android:layout_marginTop="32dp"
          android:text="Set" />

          <TextView
          android:id="@+id/textViewStatus"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_alignLeft="@+id/textView1"
          android:layout_alignRight="@+id/textView1"
          android:layout_below="@+id/textView1" />

        </RelativeLayout>

    The layout file 'activity_main.xml' should now look like:

    ![img](images/MxPowerManagerTutorialImages/activity_main.jpg)

6. Get the reference of UI elements and make a call to 'addSetButtonListener' method in 'onCreate' method. We would add this method in the next step. The method 'addSetButtonListener' creates on Click Listener for the Set Button that implements Power Manager settings selected by user. 

        :::java
        // References of the UI elements
		statusTextView = (TextView) findViewById(R.id.textViewStatus);
		pwrRadioGroup = (RadioGroup) findViewById(R.id.radioGroupPwr);
		zipFilePathEditText = (EditText) findViewById(R.id.et_zip_file_path);

		// Set on Click listener to the set button to execute Power Manager
		// operations
		addSetButtonListener();
 
     So the complete `onCreate` method looks like:

    ![img](images/MxPowerManagerTutorialImages/complete_on_create.jpg)

7. It shows an error on the method call of 'addSetButtonListener' because we have not yet added this method. We would now add the 'addSetButtonListener' method that implements on click listener of the radio buttons that are assigned to each of the Power Manager feature. As explained earlier, it sets an integer code (1-Sleep, 4-Reboot or 8-OS Update) in the variable 'value' and then calls 'modifyProfile_XMLString' method that actually modifies the Profile settings based on this value and configures the device against that Power Manager feature.

        :::java
        // Method to set on click listener on the Set Button
	    private void addSetButtonListener() {

		 // Get Reference to the Set Button
		 Button setButton = (Button) findViewById(R.id.buttonSet);

		 // On Click Listener
		 setButton.setOnClickListener(new OnClickListener() {

		 	@Override
			public void onClick(View arg0) {
				// TODO Auto-generated method stub

				// Get Reference to the Radio Buttons that show various Power
				// Manager Options
				int radioid = pwrRadioGroup.getCheckedRadioButtonId();

				if (radioid == R.id.radioSuspend)
					value = 1; // 1 - Suspend/ Sleep Mode (Set device to the
								// sleep mode)

				if (radioid == R.id.radioReset)
					value = 4; // 4 - Perform Reset/Reboot (Reboot Device)

				if (radioid == R.id.radioOSUpdate)
					value = 8; // 8 - Perform OS Update

				// Apply Settings selected by user
				modifyProfile_XMLString();
			}
		 });

	    }

    So the method looks like:

    ![img](images/MxPowerManagerTutorialImages/add_set_button_listener.jpg)
   
8. The above code would display error at the call of `modifyProfile_XMLString` method as we have not added that method yet. This is the method that actually modifies the Power Manager Profile Settings and configures the device with the user selected Power Manager feature (Sleep Mode, Reboot or OS Update). This method prepares the xml input for the `processProfile` method based on "value" attribute. If the value is 1 or 4 (Sleep Mode or Reboot), then the XML input remains the same except value attribute. If the value is 8 (OS Update), we need to add path to the OS Update package in XML input. So the XML input for this case would be different as explained in the `If-Else` condition of the code. We would capture that path from the Edit Text and store it to the `zipFilePath` variable.

    Following is an example of XML input for OS Update feature of Power Manager where the `zipFilePath` variable contains the path of the update package.

        :::java
        modifyData[0] = <?xml version=\"1.0\" encoding=\"utf-8\"?>"
		+ "<characteristic type=\"Profile\">"
		+ "<parm name=\"ProfileName\" value=\"PowerManagerProfile\"/>"
		+ "<characteristic type=\"PowerMgr\">"
		+ "<parm name=\"ResetAction\" value=\"" + value
		+ "\"/>" + "<characteristic type=\"file-details\">"
		+ "<parm name=\"ZipFile\" value=\"" + zipFilePath
		+ "\"/>" + "</characteristic>" + "</characteristic>"
		+ "</characteristic>

    The `processProfile` method then sets the changes to `Profile Manager` and returns the result to the `EMDKResults`, which is then updated in the status Text View:

        :::java
        // Method that applies the modified settings to the EMDK Profile based on
	    // user selected options of Power Manager feature.
	    private void modifyProfile_XMLString() {

		statusTextView.setText("");
		try {

			// Prepare XML to modify the existing profile
			String[] modifyData = new String[1];
			if (value == 8) {
				zipFilePath = zipFilePathEditText.getText().toString();
				// If the OS Package path entered by user is empty then display
				// a Toast
				if (TextUtils.isEmpty(zipFilePath)) {
					Toast.makeText(MainActivity.this, "Incorrect File Path...",
							Toast.LENGTH_SHORT).show();
					return;
				}

				// Modified XML input for OS Update feature that contains path
				// to the update package
				modifyData[0] = "<?xml version=\"1.0\" encoding=\"utf-8\"?>"
						+ "<characteristic type=\"Profile\">"
						+ "<parm name=\"ProfileName\" value=\"PowerManagerProfile\"/>"
						+ "<characteristic type=\"PowerMgr\">"
						+ "<parm name=\"ResetAction\" value=\"" + value
						+ "\"/>" + "<characteristic type=\"file-details\">"
						+ "<parm name=\"ZipFile\" value=\"" + zipFilePath
						+ "\"/>" + "</characteristic>" + "</characteristic>"
						+ "</characteristic>";
			} else {
				// Modified XML input for Sleep and Reboot feature based on user
				// selected options of radio button
				// value = 1 -> Sleep Mode
				// value = 4 -> Rebbot
				modifyData[0] = "<?xml version=\"1.0\" encoding=\"utf-8\"?>"
						+ "<characteristic type=\"Profile\">"
						+ "<parm name=\"ProfileName\" value=\"PowerManagerProfile\"/>"
						+ "<characteristic type=\"PowerMgr\">"
						+ "<parm name=\"ResetAction\" value=\"" + value
						+ "\"/>" + "</characteristic>" + "</characteristic>";
			}

			// Call process profile to modify the profile of specified profile
			// name
			EMDKResults results = profileManager.processProfile(profileName,
					ProfileManager.PROFILE_FLAG.SET, modifyData);

		    // Check the return status of processProfile
			if (results.statusCode == EMDKResults.STATUS_CODE.SUCCESS) {

				// Set Success Status
				resultString = "Profile update success.";

		 	} else {

				// Set Failure Status
				resultString = "Profile update failed.";
			}

		   } catch (Exception ex) {

			resultString = ex.getMessage();
		 }

		 // Display the status
		 statusTextView.setText(resultString);
	    }

    You can see that the error is gone once we add this method.
    The method `modifyProfile_XMLString` method should look like: 

    ![img](images/MxPowerManagerTutorialImages/modifyProfile_XMLString.jpg) 

8. If the EMDK is closed abruptly, a callback is  by the `onClosed` method where we would now update the status accordingly by adding following lines:

        :::java
        // This callback will be issued when the EMDK closes abruptly.
		statusTextView.setText("EMDK closed abruptly.");

    So the `onClosed` method now looks like:

    ![img](images/MxPowerManagerTutorialImages/on_closed_method.jpg)

That's it!!! We are done with all the coding and configuration part. Now let us run the application.
 

## Running the Application

1. Connect Motorola Solutions Android device (having the latest EMDK runtime) to the USB port. 

    > Note:   
    > Make sure the device is in USB debug.

2. Run the application. Since we have set `Do Nothing` parameter in the Profile Manager wiazrd, the app just loads and performs no operations. So you can see the main page with three radio button options (Sleep Mode, Reboot and OS Update).
  
	![img](images/MxPowerManagerTutorialImages/home_screen.png)
  
4. Now we will select these options one by one. So select "Suspend" radio button and press the "Set" button. This will put your device into sleep mode by locking it.

    ![img](images/MxPowerManagerTutorialImages/sleep_mode.png)

    As you can see, the device has been locked. So unclock it and the app will be resumed.
  
	![img](images/MxPowerManagerTutorialImages/sleep_mode_resumed.png)

5. So now select second option (Reboot) and press the "Set" button. This should reboot your Motorola Enterprise Android device.
 
	![img](images/MxPowerManagerTutorialImages/reboot_mode.png)

6. As the device was rebooted in the previous step, open the app again and select the third option (OS Update). Provide the path in the Edit Text to the external SD card where the OS Update Package is located. This package should be a zip file downloaded from [this link](https://portal.motorolasolutions.com/Support/US-EN/Mobile+Networks+RFID+and+BarCode+Scanners/Mobile+Computers/Handheld+Computers/TC55) (Ex. /sdcard/T55N0JB0VRUEN17400.zip).

    > Note: This above link provides the Update Packages of Motorola TC55 device only. If you are using some other Motorola Enterprise Android device then download the respective update package from [here](https://portal.motorolasolutions.com/Support/US-EN/Mobile+Networks+RFID+and+BarCode+Scanners/Mobile+Computers/Handheld+Computers)

    This package could be an OS upgrade, Factory Reset or Enterprise Reset package as this feature allows you to perform all these operations. We will be using an update Package that has been downloaded from above link for Motorola TC55 device. 

    ![img](images/MxPowerManagerTutorialImages/os_update_path.png)

    Once the "Set" button is pressed, the phone will shut down for performing OS update with the respective update package.

    > Note:
    > In case of failure due to incorrect path, the app will display a failure message in the status Text View at the bottom.

    ![img](images/MxPowerManagerTutorialImages/performing_os_update.png)

    Finally the device reboots to configure and apply the OS update changes.

    ![img](images/MxPowerManagerTutorialImages/after_os_update.png)   

##Important Programming Tips##

1. It is required to do the following changes in the application's AndroidManifest.xml:  
  
    >Note:
    >* Include the permission for EMDK:  
    
        :::xml
        <uses-permission android:name="com.symbol.emdk.permission.EMDK"/>
    
	>Note:
    >* Use the EMDK library:  
    
        :::xml
        <uses-library android:name="com.symbol.emdk"/>
  
2. Installing the EMDK for Android application without deploying the EMDK runtime on the Motorola Solutions Android  device will fail because of missing shared library on the device.
 
4. Use the DataWedge v1.7.12 or higher version to test the ProfileManager.processProfile() for DataWedge profiles.

## What's Next
Now that you have learned how to configure and perform Power Management operations on your Motorola Enterprise Android devices through applications using Mx Power Manager feature, let us try to understand and implement some of the other Mx features. So in the next tutorial, we will concentrate on the "Persist Manager" feature and try to explore this feature by creating a tutorial.

## Download the Source
The project source to this tutorial can be [downloaded (Internet Connection Required)](https://s3.amazonaws.com/emdk/Tutorials/EMDKMxAppManagerTutorial.zip).