# Bluetooth Filter

The Bluetooth Filter library allows for a more fine grained discovery of Bluetooth devices. Developed with purpose-build Android application were they connect to one or two specific Bluetooth devices in mind. The Bluetooth Filter library allows those apps to only provide a minimum list of results to their users instead of the usual general list of all devices found. 

---

## How to Use 

### Step 1

Include the below dependencies in your `build.gradle` project.

```gradle
buildscript {
    repositories {
        google()
        jcenter()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local" }
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.2'
        classpath 'com.newtronlabs.android:plugin:4.0.5'
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        maven { url "https://newtronlabs.jfrog.io/artifactory/libs-release-local" }
    }
}

subprojects {
    apply plugin: 'com.newtronlabs.android'
}
```

In the `build.gradle` of your app.

```gradle
dependencies {
    compileOnly 'com.newtronlabs.bluetoothfilter:bluetoothfilter:4.0.0'
}
```


### Step 2

Implement the `IDiscoveryListener`

```java
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
https://gist.github.com/NewtronLabs/216f45db2339e0bc638e7c14a6af9cc8


## Contact

solutions@newtronlabs.com

