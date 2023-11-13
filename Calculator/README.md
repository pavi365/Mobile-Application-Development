## Ex.No:9 Develop a simple calculator using android studio.

## AIM:

To develop a program to develop a simple calculator in Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as calculator and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout using UI components in activity_main.xml.

Step 6: Display the calculator operation in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
Activity_main.xml:
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
```
xmlns:app="http://schemas.android.com/apk/res-auto"

xmlns:tools="http://schemas.android.com/tools"

android:layout_width="match_parent"

android:layout_height="match_parent"

tools:context=".MainActivity">

<Button
    android:id="@+id/button"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginTop="72dp"
    android:onClick="onFetchContactsClicked"
    android:text="Fetch Contacts"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintHorizontal_bias="0.497"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />

<TextView
    android:id="@+id/textView"
    android:layout_width="0dp"
    android:layout_height="0dp"
    app:layout_constraintTop_toBottomOf="@id/button"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintBottom_toBottomOf="parent"
    android:layout_marginTop="16dp"
    android:textAppearance="?android:textAppearanceMedium" />
```
</androidx.constraintlayout.widget.ConstraintLayout>

MainActivity.java:
package com.example.myapplication;

import androidx.annotation.NonNull;

import androidx.appcompat.app.AppCompatActivity;

import androidx.core.app.ActivityCompat;

import androidx.core.content.ContextCompat;

import android.Manifest;

import android.content.pm.PackageManager;

import android.database.Cursor;

import android.net.Uri;

import android.os.Bundle;

import android.provider.ContactsContract;

import android.widget.Button;

import android.widget.TextView;

import android.widget.Toast;

public class MainActivity extends AppCompatActivity { private static final int REQUEST_READ_CONTACTS = 1; Button btnFetchContacts; TextView txtContacts;
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    btnFetchContacts = findViewById(R.id.button);
    txtContacts = findViewById(R.id.textView);

    btnFetchContacts.setOnClickListener(v -> {
        if (ContextCompat.checkSelfPermission(MainActivity.this,
                Manifest.permission.READ_CONTACTS) != PackageManager.PERMISSION_GRANTED) {
            ActivityCompat.requestPermissions(MainActivity.this,
                    new String[]{Manifest.permission.READ_CONTACTS},
                    REQUEST_READ_CONTACTS);
        } else {
            fetchContacts();
        }
    });
}

private void fetchContacts() {
    StringBuilder contactsBuilder = new StringBuilder();
    Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;
    String[] projection = {ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME,
            ContactsContract.CommonDataKinds.Phone.NUMBER};

    Cursor cursor = getContentResolver().query(uri, projection, null, null, null);

    if (cursor != null) {
        int nameIndex = cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME);
        int numberIndex = cursor.getColumnIndex(ContactsContract.CommonDataKinds.Phone.NUMBER);

        while (cursor.moveToNext()) {
            if (nameIndex != -1 && numberIndex != -1) {
                String name = cursor.getString(nameIndex);
                String number = cursor.getString(numberIndex);
                contactsBuilder.append(name).append(" - ").append(number).append("\n");
            }
        }
        cursor.close();

        txtContacts.setText(contactsBuilder.toString());
    }
}

@Override
public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
    super.onRequestPermissionsResult(requestCode, permissions, grantResults);

    if (requestCode == REQUEST_READ_CONTACTS) {
        if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            // Permission is granted, fetch contacts
            fetchContacts();
        } else {
            // Permission is denied, show a toast message
            Toast.makeText(this, "Permission denied", Toast.LENGTH_SHORT).show();
        }
    }
}
}
AndroidManifest.xml:
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
```
xmlns:tools="http://schemas.android.com/tools">

<uses-permission android:name="android.permission.READ_CONTACTS" />
<application
    android:allowBackup="true"
    android:dataExtractionRules="@xml/data_extraction_rules"
    android:fullBackupContent="@xml/backup_rules"
    android:icon="@mipmap/ic_launcher"
    android:label="@string/app_name"
    android:supportsRtl="true"
    android:theme="@style/Theme.MyApplication"
    tools:targetApi="31">
    <activity
        android:name=".MainActivity"
        android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />

            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
```
Developed by:P.Pavithra
RegisterNumber:212221220037

## OUTPUT

![mad-1](https://github.com/pavi365/Mobile-Application-Development/assets/115135775/f9f5d3ff-659f-4f8c-9b57-bf162b603a91)

![mad-2](https://github.com/pavi365/Mobile-Application-Development/assets/115135775/1dd5db18-6726-491e-a9cc-5b1c34fc5633)







## RESULT
Thus a Simple Android Application develop a program to create simple calculator in Android Studio is developed and executed successfully.
