# Bluetooth Filter

The Bluetooth Filter library allows for a more fine grained discovery. Developed with purpose-build Android application where they connect to one or two specific Bluetooth devices in mind. The Bluetooth Filter library allows those apps to only provide a minimum list of results to their users rather instead of the usual general list of all devices found. 

---

## How to Use 

### Step 1

Include the below dependencies in your `build.gradle` project.

```
allprojects {
    repositories {
        jcenter()
        maven { url "http://code.newtronlabs.com:8081/artifactory/libs-release-local" }
    }
}
```

In the `build.gradle` of your app.

```
compile 'com.newtronlabs.bluetoothfilter:bluetoothfilter:1.1.0'
```


### Step 2

Implement the `IDiscoveryListener`

```android
public class MainActivity extends AppCompatActivity implements IDiscoveryListener
{
    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    @Override
    protected void onResume()
    {
        super.onResume();

        List<IDeviceFilter> filterList = new ArrayList<IDeviceFilter>();
        
        // Discover any BT Device with an address starting with 0.
        filterList.add(new NameAddressFilter("XYZ Random", ".*", "0.*"));
        FilterBluetoothAdapter.getAdapter().startDiscovery(this, filterList, this);
    }

    @Override
    public void onDiscoveryStarted()
    {
        Log.d("Test", "Discovery Started");
    }

    @Override
    public void onDeviceFound(IDevice deviceFound)
    {
        Log.d("Test", "Device Found: Class - " 
             + deviceFound.getClassification() + " Dev: " + deviceFound.getDevice());
    }

    @Override
    public void onDiscoveryFinished()
    {
        Log.d("Test", "Discovery Finished");
    }
}
```

---

## License

Bluetooth Filter binaries and source code can only be used in accordance with Freeware license. That is, freeware may be used without payment, but may not be modified. The developer of Bluetooth Filter retains all rights to change, alter, adapt, and/or distribute the software. Bluetooth Filter is not liable for any damages and/or losses incurred during the use of Bluetooth Filter.

Users may not decompile, reverse engineer, pull apart, or otherwise attempt to dissect the source code, algorithm, technique or other information from the binary code of Bluetooth Filter unless it is authorized by existing applicable law and only to the extent authorized by such law. In the event that such a law applies, user may only attempt the foregoing if: (1) user has contacted Newtron Labs to request such information and Newtron Labs has failed to respond in a reasonable time, or (2) reverse engineering is strictly necessary to obtain such information and Newtron Labs has failed to reply. Any information obtained by user from Newtron Labs may be used only in accordance to the terms agreed upon by Newtron Labs and in adherence to Newtron Labs confidentiality policy. Such information supplied by Newtron Labs and received by user shall not be disclosed to a third party or used to create a software substantially similar to the technique or expression of the Newtron Labs Bluetooth Filter software.


## Contact

contact@newtronlabs.com

