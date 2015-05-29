# Using Multiple Data Capture Profiles
## Developing an EMDK for Android Application Part 3

This guide will walk you through adding MSR support and multiple profiles to the Android application you made using [Developing an EMDK for Android Application Part 2](../guide/tutorial/tutdatacaptureprofilept2). This tutorial will add some more complexity by adding a second screen as well as adding a second Data Capture Profile.

###Prerequisites

* Java Development Kit (JDK)
* Android Developer Tools (ADT)
* Motorola EMDK for Android 
* Completion of [Developing an EMDK for Android Application Part 1](../guide/tutorial/tutdatacaptureprofile)
* Completion of [Developing an EMDK for Android Application Part 2](../guide/tutorial/tutdatacaptureprofilePt2)
 
For more information about setting up the EMDK please see the EMDK [Setup](../guide/setup).

##Adding MSR Activity
Let's start by defining a second activity for the application. This activity will be used to to activate a Data Capture profile that listens for MSR data.

1. Select "EMDKSample" from "Package Explorer" in Eclipse.  
    ![img](images/setup/image122.jpg)  
2. Right Click and select "New" -> "Other".  
    ![img](images/setup/image123.jpg)  
3. Select "Android" -> "Android Activity" and click "Next".  
    ![img](images/setup/image124.jpg)  
4. Select "Empty Activity" and click "Next".  
    ![img](images/setup/image125.jpg)  
5. Change "Activity name" to "MSRActivity" and click "Finish".  
    ![img](images/setup/image126.jpg)  

##Adding MSR Completed Activity
Next let's create a third activity that will listen for the MSR data and display the data to the user.

1. Select "EMDKSample" from "Package Explorer" in Eclipse.  
    ![img](images/setup/image122.jpg)  
2. Right Click and select "New" -> "Other".  
    ![img](images/setup/image123.jpg)  
3. Select "Android" -> "Android Activity" and click "Next".  
    ![img](images/setup/image124.jpg)  
4. Select "Empty Activity" and click "Next".  
    ![img](images/setup/image125.jpg)  
5. Change "Activity name" to "MSRCompletedActivity" and click "Finish".  
    ![img](images/setup/image127.jpg)  

##Updating Main Activity
Now we will update "MainActivity", adding a button to launch our "MSRActivity".

1. Select "activity_main.xml" from "Package Explorer" in Eclipse.  
	![img](images/setup/image128.jpg)  
2. Add the following Button to "activity_main.xml". This Button will be used for opening "MSRActivity".  
	
        :::xml
        <Button  
        android:id="@+id/buttonMSR"  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:layout_alignParentBottom="true"  
        android:layout_marginBottom="50dp"  
        android:layout_marginLeft="50dp"  
        android:text="MSR" />

	![img](images/setup/image129.jpg)  
3. Select "MainActivity.java" from "Package Explorer" in Eclipse. 

	![img](images/setup/image130.jpg) 
4. Add the following Imports to "MainActivity.java".  
	
        :::java
        import android.widget.Button;  
        import android.view.View;  
        import android.view.View.OnClickListener; 

	![img](images/setup/image131.jpg)  
5. Declare a variable inside "MainActivity" to store "buttonMSR". 
	
        :::java
        //Declare a variable to store the buttonMSR  
        private Button buttonMSR = null;  

	![img](images/setup/image132.jpg)  
6. Inside "onCreate" get a reference to "buttonMSR".
	
        :::java
        //Declare a variable to store the buttonMSR  
        private Button buttonMSR = null; 

	![img](images/setup/image133.jpg)  
7. Inside "onCreate" add an "OnClickListener" for "buttonMSR".  
	
        :::java
        //Add an OnClickListener for buttonMSR  
        buttonMSR.setOnClickListener(buttonMSROnClick);     

	![img](images/setup/image134.jpg)  

8. Add a new "OnClickListener" inside "MainActivity". 

        :::java
        //OnClickListener for buttonMSR  
        private OnClickListener buttonMSROnClick = new OnClickListener() {  
            public void onClick(View v) {  
          
            }  
        };  

	![img](images/setup/image135.jpg)  
9. Add the following code to "onClick" to launch "MSRActivity". 

        :::java
        //Launch MSRActivity  
        Intent myIntent = new Intent(MainActivity.this, MSRActivity.class);  
        startActivity(myIntent);  

	![img](images/setup/image136.jpg) 

##Creating MSR UI
Next we will create the UI for "MSRActivity". 

1. Select "activity_msr.xml" from "Package Explorer" in Eclipse.  
	![img](images/setup/image137.jpg) 
2. Remove the default "TextView". 
3. Add the following TextView. 

        :::xml
        <TextView  
            android:id="@+id/textViewInfo"  
            android:layout_width="wrap_content"  
            android:layout_height="wrap_content"  
            android:layout_alignParentTop="true"  
            android:layout_centerHorizontal="true"  
            android:layout_marginTop="50dp"  
            android:text="Please swipe a card to continue."  
            android:textAppearance="?android:attr/textAppearanceLarge" /> 

	![img](images/setup/image138.jpg) 

##Creating our MSR Profile
Next we will create a Data Capture profile that will activate the MSR on "MSRActivity" and send the data via a startActivity Intent to "MSRCompletedActivity".  

1. Select "EMDKSample" project from Package Explorer.    
2. Click "EMDK" menu and select "Profile Manager".  
    ![img](https://launchpad-images.s3-us-west-1.amazonaws.com/emdk/setup/image043.jpg)  
3. The EMDK Profile Manager Window will appear.  
    ![img](images/setup/image139.jpg)  
4. click "Create".  
    ![img](images/setup/image140.jpg)  
5. Enter the Profile Name "DataCaptureProfileMSR" and click "Create".  
    ![img](images/setup/image141.jpg)  
6. select "ActivitySelection" from the list of "Available Features" and add it to "Selected Features" using the arrow.  
    ![img](images/setup/image142.jpg)  
7. Select "Activity Selection".  
    ![img](images/setup/image143.jpg)  
8. Enter "com.symbol.emdksample" as the application name and click apply.  
    ![img](images/setup/image144.jpg)  
9. Enter "MSRActivity" as the activity name and click apply.  
    ![img](images/setup/image145.jpg)  	
10. Click Okay.  
11. select "MSR" from the list of "Available Features" and add it to "Selected Features" using the arrow. 
    ![img](images/setup/image146.jpg)  	
12. Change "MSR Input Enable" to "Enable".  
	![img](images/setup/image147.jpg) 
13. select "Intent" from the list of "Available Features" and add it to "Selected Features" using the arrow. 
	![img](images/setup/image148.jpg) 
14. Now we will configure the "Intent" settings.  
	* Switch "Intent Output Enable" to Enable". 
	* For "Intent Output Action" enter "com.symbol.emdksample.RECVRMSR".
	* For "Intent Output Category" enter "android.intent.category.DEFAULT".
	* Switch "Intent Output Delivery" to "Send via startActivity".  
	* Switch "Basic data formatting Enable" to Enable". 
	* Switch "Basic data formatting Send Data" to Enable". 	

	Your Intent configuration should now look like this:  
	![img](images/setup/image149.jpg)  

15. Click "Apply" and "Finish".  
    ![img](images/setup/image150.jpg)  
16. Click "Close".  
    >Note:  
    >Now the "EMDKConfig.xml" file under the "\assets" folder will be updated with your changes.

##Adding the MSR Intent Filter
Now will add an Intent filter to our Manifest file to allow "MSRCompletedActivity" to listen for our new Data Capture Intent. 

1. Open your application's "Manifest.xml" file.  
	![img](images/setup/image151.jpg)
2. Add the following configuration to the activity "com.symbol.emdksample.MSRCompletedActivity" to revive our MSR intent.  

        :::xml	 
        <intent-filter>  
                <action android:name="com.symbol.emdksample.RECVRMSR"/>  
                <category android:name="android.intent.category.DEFAULT"/>  
        </intent-filter>  

    When done, your manifest.xml should look like this:

    ![img](images/setup/image152.jpg)  

	>Note:  
	>
	>* The intent action name should match the value of "Intent Output Action" in the EMDK Profile Manager. 
	>* The intent category name should match the value of "Intent Output Category" in the EMDK Profile Manager.

##Registering the MSR EMDK profile
Next we will register our new Data Capture profile from "MainActivity".

1. Select "MainActivity.java" from "Package Explorer" in Eclipse. 

	![img](images/setup/image153.jpg) 
2. Inside "MainActivity" add the following code to hold the name of our MSR profile.  

        :::java
        //Assign the profile name used in EMDKConfig.xml  for MSR handling  
        private String profileNameMSR = "DataCaptureProfileMSR";  

    ![img](images/setup/image154.jpg)  
3. Inside "onOpened" add the following code to register the MSR EMDK profile. 

        :::java
        //Call processPrfoile for profile MSR  
        results = mProfileManager.processProfile(profileNameMSR, ProfileManager.PROFILE_FLAG.SET, modifyData);  
          
        if(results.statusCode == STATUS_CODE.FAILURE)  
        {  
        //Failed to set profile MSR  
        }  

    ![img](images/setup/image155.jpg)  

##Creating MSR Completed UI
Now we will create the UI for "MSRCompletedActivity". This UI will allow us to display the MSR data to the user.

1. Select "activity_msr.xml" from "Package Explorer" in Eclipse.  
	![img](images/setup/image156.jpg) 
2. Remove the default "TextView". 
3. Add the following TextView. 

    :::xml
    <TextView  
        android:id="@+id/textViewMSRData"  
        android:layout_width="wrap_content"  
        android:layout_height="wrap_content"  
        android:layout_alignParentTop="true"  
        android:layout_centerHorizontal="true"  
        android:layout_marginTop="50dp"  
        android:text="Data = "  
        android:textAppearance="?android:attr/textAppearanceMedium" />  

	![img](images/setup/image157.jpg) 

##Handling MSR Intents
Next will will add the code to "MSRCompletedActivity" for capturing the startActivity Intent and displaying the result data to the user. 

1. Select "MSRCompletedActivity.java" from "Package Explorer" in Eclipse. 

	![img](images/setup/image158.jpg) 
2. Add the following imports.  

        :::java
        import android.content.Intent;  
        import android.widget.TextView; 

	![img](images/setup/image159.jpg)  
3. Add the following function for processing intents.  

        :::java
        //This function is responsible for getting the data from the intent  
        private void handleDecodeData(Intent i)  
        {  
          
        }  
     
    ![img](images/setup/image160.jpg)  
4. Add the following code to your "onCreate" function to check for a possible intent;  

        :::java
        //In case we have been launched by the DataWedge intent plug-in  
        Intent i = getIntent();  
        handleDecodeData(i);
     
    ![img](images/setup/image161.jpg)  
5. Overide "onNewIntent" to handle incoming intents.  

        :::java
        //We need to handle any incoming intents, so let override the onNewIntent method  
        @Override  
        public void onNewIntent(Intent i) {  
            handleDecodeData(i);  
           
        }
     
    ![img](images/setup/image162.jpg)  
6. Add a global variable for the TextView. 

        :::java
        //Declare a variable to store the textViewMSRData  
        private TextView textViewMSRData = null; 
	
	![img](images/setup/image163.jpg)  
7. Add the following code to your onCreate function to get a handle on the TextView.
 
        :::java
        //Get the textViewBarcode  
        textViewMSRData = (TextView) findViewById(R.id.textViewMSRData); 

	![img](images/setup/image164.jpg)   
8. Add the following code to your "handleDecodeData" function to confirm the intent was meant for us. 

        :::java
        //Check the intent action is for us  
        if (i.getAction().contentEquals("com.symbol.emdksample.RECVRMSR"))  
        {  
          
        }
    
    ![img](images/setup/image165.jpg)   
9. Add the following code to your "handleDecodeData" function to check if the intent contains MSR data.  

        :::java
        //Get the source of the data  
        String source = i.getStringExtra("com.motorolasolutions.emdk.datawedge.source");  
          
             
        //Check if the data has come from the msr  
        if(source.equalsIgnoreCase("msr"))  
        {  
          
        }  

	![img](images/setup/image166.jpg)  
10. Add the following code to your "handleDecodeData" function to retrieve MSR data.  

        :::java
        //Get the data from the intent  
        String data = i.getStringExtra("com.motorolasolutions.emdk.datawedge.data_string");  
          
        //Check that we have received data  
        if(data != null && data.length() > 0)  
        {  
          
        }

	![img](images/setup/image167.jpg)
11. Add the following code to your "handleDecodeData" function to populate the TextView with the revived MSR data.

        :::java
        //Display the data to textViewMSRData  
        textViewMSRData.setText("Data = " + data);  

	![img](images/setup/image168.jpg) 

##Running the Application
Lastly we will run and test our application. 

1. Connect Motorola Solutions Android device (having the latest EMDK runtime) to the USB port.

    >Note:   
    >Make sure the device is in USB debug.

2. Run the application.  

	![img](images/setup/image169.png) 
3. Press the trigger button and scan a Barcode. 
4. Like before the scanned data will be populated in the Edit Text field Through the previous Keystroke Intent and will appear on the Text View using the previous Datawedge Intent.   

	![img](images/setup/image170.png) 
5. Press the button "MSR".  

	![img](images/setup/image171.png)
6. Swipe a cad through the MSR.  

	![img](images/setup/image172.png)
7. Press return to go back to the MSR where you can swipe another card, or hit return again to go back to the main screen. 

## What's Next
The [next tutorial](../guide/tutorial/tutdatacaptureprofilePt4) will show you how to use the Intent Output as a Broadcast instead of starting an activity.

## Download the Source
The project source to this tutorial can be [downloaded (Internet Connection Required)](https://s3.amazonaws.com/emdk/Tutorials/EMDK-UsingMultipleDataCaptureProfiles.zip).