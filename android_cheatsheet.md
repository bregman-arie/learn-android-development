## Android Cheat Sheet

Note: all the examples use Kotlin and not Java.

* [Buttons](#buttons)
* [Colors](#colors)
* [EditText](#EditText)

### Activities

#### First steps in "Empty Activity"

Create a layout:

1. Right click on "res" folder  -> new -> Android resource directory.
2. Name it "layout" and also change its type to "layout". Click on "OK" which should create the layout directory

Next create a basic activity

1. Right click on the new "layout" directory ->  new -> Activity -> Empty Activity

Add default activity to manifest:

1. Click on Manifests directory -> AndroidManifest.xml
2. Insert the following :

```kotlin
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>
</activity>
```

#### Move between activities

```kotlin
val intent = Intent(context,<activity_name>::class.java)
intent.putExtra("var_name", "var_value")
context!!.startActivity(intent)
```

### Gradle

* Apply changes: click on terminal -> insert `gradlew clean` and press ctrl + enter

### Text

* Change text: `textID.text = "some text"`
* Center text: in the IDE menu click on`Attributes -> gravity -> center`

### Buttons

##### Run code upon clicking on a button - Listener way (Preferred)

Go to main activity and under the main activity class, add this

```kotlin
<button_id>.setOnClickListener{
    // Add code to execute when the button is clicked on
}    
```

##### Run function upon clicking on a button - UI way

In the UI, set onClick to "change" and add the following function

```kotlin
fun change(view: View) {

    }
```

##### Change image upon clicking on a button with the id "change"

Note: onClick is set to "change"

```
fun change(view: View) {
    imageView.setImageResource(R.drawable.<image_name>)
}
```

##### Change text upon clicking on a button (the text ID is "textView")

```
fun update(view: View) {
    textView.text = "text changed! :)"
}
```

##### Layout Width

* wrap content - the width of the button will be set based on the content (length of the text for example)
* match parent - the width will be based on the width of the parent in component tree
* Use "pt" measurement for setting the width or height of components (e.g. 30pt)

##### Share Button

```kotlin
binding.shareButton.setOnClickListener {
            val shareIntent = Intent().apply {
                this.action = Intent.ACTION_SEND
                this.putExtra(Intent.EXTRA_TEXT, "Check out this app on Google Play\n\n" +
                        "http://play.google.com/store/apps/details?id=com.X.Y")
                this.type = "text/plain"

            }
            startActivity(shareIntent)
        }
```

##### Rate Button

```kotlin
binding.rateButton.setOnClickListener {
            val rateIntent = Intent(Intent.ACTION_VIEW, Uri.parse("market://details?id=com.X.Y"))
            startActivity(rateIntent)
        }
```

### Input

##### Add input field 

```
Palette -> Text -> Plain Text
```

* Change input type: `Attributes -> inputType`

* Hint (input text disappears as soon as the user starts typing)

```
Attributes -> EditText -> hint -> put your text
Attributes -> TextView -> text -> remove text
```

##### Get text from input field

The id of the input field is x

```
// string
val userInput = x.text.toString()
// integer
val userInput = Integer.parseInt(x.text.toString())
```

### Date | Calendar

##### Get current year

```kotlin
import java.util.*
val currentYear = Calendar.getInstance().get(Calendar.YEAR)
```

### Debugging

##### UI

1. You click on the line number to add a breakpoint
2. Click on "debug" button to start running (Bug icon, Shift + F9)

##### Logging

You can log messages and see them when clicking on "Logcat" in the IDE.

```kotlin
import android.util.Log
Log.d("Log Tag", "Hey, you logged this line")
```

### Table

##### Center all the elements in a table row

```kotlin
<TableRow
    android:gravity="center"
    ...
// Same can be added to table layout to center everything in a table
```

### Colors

##### Define a new color

1. Go to res -> values -> colors.xml
2. Add a new line like: `<color name="colorAccent">#03DAC5</color>`
3. You can now use reference it this way: `"@color/colorAccent"`

### Images

#### Add images

Drag and drop images to res -> drawable (if drawable doesn't exists then right click on "res" -> new -> Android Resource Directory)

#### Use Images

```
R.drawable.<image_name>
```

#### Set a different image

```kotlin
binding.someImageView.setImageResource(R.drawable.someOtherImage)
```

### Toasts

##### Show toast for a long time

````kotlin
Toast.makeText(this, "Wow!", Toast.LENGTH_LONG).show()
````

### Migrate to New Binding

1. Add to build.gradle (module level) the following

```
buildFeatures {
    viewBinding true
}
```

2. In MainActivity add and change the following

```
class MainActivity : AppCompatActivity() {

    private lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding  = ActivityMainBinding.inflate(layoutInflater)
        setContentView(binding.root)
```

### EditText

#### Example

```xml
<EditText
    android:id="@+id/playerName"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:textSize="32sp"></EditText>
```

#### Disable Editing

```xml
 android:enabled="false"
```

#### Hide Underline

```xml
android:background="@android:color/transparent"
```

#### Limit number of characters

```
android:maxLength="10"
```

#### Activate Disabled EditText

```kotlin
binding.someEditText.isFocusable=true
binding.someEditText.isEnabled=true
binding.someEditText.isFocusableInTouchMode=true
binding.someEditText.isFocusable=true
binding.someEditText.isCursorVisible=true
binding.someEditText.requestFocus()
val inputMethodManager = this.getSystemService(Activity.INPUT_METHOD_SERVICE) as InputMethodManager
inputMethodManager.showSoftInput(it, InputMethodManager.SHOW_FORCED)
```

### Layout

#### Linear Layout

Go to res -> layout -> activity_main.xml and in "Text" change it to

```
LinearLayout
```

### Hardware Profiles

Unfortuantely it doesn't seems there is a site with a collection of hardawre profiles, so if you would like to have an hardware profile for an existing phone, you'll have to create a new hardware profile

```
AVD manager -> Create Virtual Device... -> New Hardware Profile
```

### Support Multiple Screens

1. Right click on layout directory 
2. New -> Layout Resource File 
3. Name it the same "activity_main" 
4. In directory name append "-mdpi" or any other screen size you would like to support

### Convert Java to Kotlin

```
ctrl + shift + a -> convert java file to kotlin
```

### Check and ask for permissions

```
if(ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)!= PackageManager.PERMISSION_GRANTED) {
                requestPermissions(arrayOf(Manifest.permission.ACCESS_FINE_LOCATION, ACCESSLOCATION))
```

### Threads

#### Communicate with the UI

Inside Thread class add the following

```
runOnUiThread {}
```

#### Sleep

Sleep for 1000 miliseconds

```
Thread.sleep(1000)
```

### Google Maps

#### API key

For an application that is using Google Maps you have to [obtain an API key](https://developers.google.com/maps/documentation/embed/get-api-key)

Once obtained, put it in google_maps_api.xml

#### Access to the internet

In order for the app work properly change this line

```
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```

to

```
<uses-permission android:name="android.permission.INTERNET" />
```

#### New Map

```
mMap = googleMap
```

#### Add marker with an image

```
val sydney = LatLng(-34.0, 151.0)
        mMap.addMarker(MarkerOptions()
                .position(sydney)
                .title("Me")
                .snippet("My Location")
                .icon(BitmapDescriptorFactory
                .fromResource(R.drawable.<IMAGE_NAME_IN_DRAWABLE_DIR>)))
```

#### Zoom on the location

```
mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(sydney,14f))
```

#### Getting the location

Add the following to AndroidManifest.xml: `<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />`

#### Before Releasing the app

Make sure to change google_maps_api.xml from debug to release. Click on "Build Variables" in left side menu and in the dropbox choose "release"

### SQL

#### DatabaseHandler Class

A class for managing Database operations (like create, insert, etc.)

```kotlin
class DatabaseHandler(context: Context) :
    SQLiteOpenHelper(context, DATABASE_NAME, null, DATABASE_VERSION) {

        companion object {
        private const val DATABASE_VERSION = 1
        private const val DATABASE_NAME = "MyDatabasse"
        private const val TABLE_PLAYER = "PlayerTable"

        private const val KEY_ID = "_id"
        private const val KEY_NAME = "name"
    }
        
        override fun onCreate(db: SQLiteDatabase?) {
            val CREATE_PLAYER_TABLE =  ("CREATE TABLE "+ TABLE_PLAYER + "("
            +KEY_ID + " INTEGER PRIMARY KEY," + KEY_NAME + " TEXT" + ")")
            db?.execSQL(CREATE_PLAYER_TABLE)
        }
}
```

#### Insert only once

This is useful for use cases like adding a player. You don't want to add a player every time a user starts the app.

The way to do it is calling the "addPlayer" function once from "onCreate" method of your Database handler class.

#### Delete Database

Delete database called "MyDatabase"

```kotlin
this.deleteDatabase("MyDatabase")
```

#### Retrieve Boolean from the Database

```kotlin
val booleanVar = cursor.getInt(SOME_KEY_IN_DB) > 0;
```