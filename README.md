
# Ex.No:3 Create Your Own Content Providers to get Contacts details.

## Developed by: Knowkash G
## Registeration Number : 212225230142


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Min. required Artic Fox)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “ex.no.3″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
### MainActivity
```
package com.example.contentprovider;

import android.app.Activity;
import android.os.Bundle;
import android.content.ContentValues;
import android.database.Cursor;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends Activity {

    EditText etName, etPhone;
    Button btnAdd, btnView;
    TextView tvResult;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_main);

        etName = findViewById(R.id.etName);
        etPhone = findViewById(R.id.etPhone);

        btnAdd = findViewById(R.id.btnAdd);
        btnView = findViewById(R.id.btnView);

        tvResult = findViewById(R.id.tvResult);

        // Add Contact
        btnAdd.setOnClickListener(v -> {

            String name = etName.getText().toString();
            String phone = etPhone.getText().toString();

            ContentValues values = new ContentValues();

            values.put(DatabaseHelper.NAME, name);
            values.put(DatabaseHelper.PHONE, phone);

            getContentResolver().insert(
                    ContactProvider.CONTENT_URI,
                    values
            );

            Toast.makeText(
                    MainActivity.this,
                    "Contact Added Successfully",
                    Toast.LENGTH_SHORT
            ).show();

            etName.setText("");
            etPhone.setText("");
        });

        // View Contacts
        btnView.setOnClickListener(v -> {

            Cursor cursor = getContentResolver().query(
                    ContactProvider.CONTENT_URI,
                    null,
                    null,
                    null,
                    null
            );

            StringBuilder result = new StringBuilder();

            if (cursor != null) {

                while (cursor.moveToNext()) {

                    String name = cursor.getString(
                            cursor.getColumnIndexOrThrow(
                                    DatabaseHelper.NAME
                            )
                    );

                    String phone = cursor.getString(
                            cursor.getColumnIndexOrThrow(
                                    DatabaseHelper.PHONE
                            )
                    );

                    result.append("Name: ")
                            .append(name)
                            .append("\n");

                    result.append("Phone: ")
                            .append(phone)
                            .append("\n\n");
                }

                cursor.close();
            }

            tvResult.setText(result.toString());
        });
    }
}
```
### Activity
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#EC8D0B"
    android:orientation="vertical"
    android:padding="20dp">

    <!-- Title -->

    <!-- Name Input -->

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:padding="16dp"
        android:text="@string/title_contact_provider"
        android:textSize="34sp"
        android:textStyle="bold" />

    <!-- Phone Input -->
    <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:autofillHints="name"
        android:hint="@string/hint_enter_name"
        android:inputType="textPersonName" />

    <EditText
        android:id="@+id/etPhone"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:autofillHints="phone"
        android:hint="@string/hint_enter_phone_number"
        android:inputType="phone" />

    <!-- Add Contact Button -->

    <!-- View Contacts Button -->

    <!-- Display Contacts -->

    <Button
        android:id="@+id/btnAdd"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:backgroundTint="#97689D"
        android:text="@string/btn_add_contact" />

    <Button
        android:id="@+id/btnView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:backgroundTint="#97689D"
        android:text="@string/btn_view_contacts" />

    <TextView
        android:id="@+id/tvResult"
        android:layout_width="match_parent"
        android:layout_height="440dp"
        android:padding="20dp"
        android:textSize="18sp" />

</LinearLayout>
```
### AndroidManifest
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.ContentProvider">
        <provider
            android:name=".ContactProvider"
            android:authorities="com.example.contentprovider.ContactProvider"
            android:exported="false" />
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:windowSoftInputMode="adjustResize">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

## OUTPUT
<img width="1901" height="1016" alt="Screenshot 2026-11-22 112950" src="https://github.com/user-attachments/assets/0aa28da3-df97-4268-980b-f9b46612bf47" />

## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.
