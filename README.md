# BMI_Tracker_App

### Nama : Sayyid Sulthan Abyan
### NIM: 312410496
### Kelas: TI.24.A.5

---

# Proyek Aplikasi Kalkulator berat badan "BMI Tracker"

Ini adalah repository untuk Proyek Ujian Tengah Semester (UTS) Mata Kuliah Pemrograman Mobile 1.

Proyek ini mencakup seluruh alur desain (UX/UI) untuk aplikasi pencatat keuangan sederhana bernama "BMI Tracker".

---

## Tentang Proyek Ini

Proyek ini adalah implementasi dari 6 poin soal UTS, yang mencakup:

1. Desain Splash Screen: Alur splash screen yang canggih dengan deteksi lokasi (GPS) untuk menampilkan bendera dan bahasa.

2. Storyboard: Alur cerita pengguna (user flow) lengkap dalam 7 frame.

3. Mockup (Wireframe): Sketsa kasar (lo-fi) tata letak aplikasi.

4. Desain UI (High-Fidelity): Desain visual final (hi-fi) aplikasi, lengkap dengan palet warna dan tipografi.

5. Prototype UX (Video): Video demonstrasi prototype interaktif yang dibuat di Figma.

7. Manajemen Proyek: Perencanaan dan pelacakan proyek menggunakan ClickUp.

---

# Video Prototype UX (.mp4):

Video rekaman layar yang mendemonstrasikan alur prototype Figma, dari membuka aplikasi hingga ujicoba hitung berat badan.

link URL YOUTUBE:
[https://youtu.be/lqH_wZOQdR0](https://youtu.be/KF4BCbQV6TA)


**(SplashScreen & Prototype.mp4)**

---

# Gambar Desain UI Final:

gambar Desain UI final (high-fidelity) dalam format 

**(Desain_UI.png.)**

🛠️ Alat yang Digunakan

Manajemen Proyek: ClickUp

Desain UX/UI & Prototyping: Figma

Penyimpanan Aset: GitHub

---
# Notifikasi 
![gambar 1](notifikasi.JPG)

---

# Implementasi android studio

## 1. Splash Screen

### Layout

**Code XML: `activity_splah.xml`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#62E0FD">

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:orientation="vertical"
        android:gravity="center">


    <ImageView
        android:id="@+id/logo"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:alpha="0"
        android:scaleX="0.2"
        android:scaleY="0.2"
        android:src="@drawable/logo_bmi" />

    <ImageView
        android:id="@+id/Shadowlogo"
        android:layout_width="80dp"
        android:layout_height="10dp"
        android:src="@drawable/shadow"
        android:layout_marginTop="20dp"
        android:alpha="0"
        android:scaleX="0.2"
        android:scaleY="0.2"/>
    </LinearLayout>

</RelativeLayout>
```

### Methode

**Java Class: `SplahsActivity.java`**

```java
package com.example.bmitracker;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.os.Handler;
import android.widget.ImageView;
import android.animation.ObjectAnimator;
import android.animation.AnimatorSet;

public class SplashActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_splash); // pastikan nama XML sesuai milikmu

        ImageView logo = findViewById(R.id.logo);
        ImageView shadowLogo = findViewById(R.id.Shadowlogo);

        // Set posisi awal (sama seperti XML yang tadi)
        logo.setAlpha(0f);
        logo.setScaleX(0.2f);
        logo.setScaleY(0.2f);

        shadowLogo.setAlpha(0f);
        shadowLogo.setScaleX(0.2f);
        shadowLogo.setScaleY(0.2f);

        // Animasi fade-in dan zoom-in
        ObjectAnimator fadeLogo = ObjectAnimator.ofFloat(logo, "alpha", 0f, 1f);
        ObjectAnimator scaleXLogo = ObjectAnimator.ofFloat(logo, "scaleX", 0.2f, 1f);
        ObjectAnimator scaleYLogo = ObjectAnimator.ofFloat(logo, "scaleY", 0.2f, 1f);

        ObjectAnimator fadeShadow = ObjectAnimator.ofFloat(shadowLogo, "alpha", 0f, 1f);
        ObjectAnimator scaleXShadow = ObjectAnimator.ofFloat(shadowLogo, "scaleX", 0.2f, 1f);
        ObjectAnimator scaleYShadow = ObjectAnimator.ofFloat(shadowLogo, "scaleY", 0.2f, 1f);

        AnimatorSet animatorSet = new AnimatorSet();
        animatorSet.playTogether(fadeLogo, scaleXLogo, scaleYLogo, fadeShadow, scaleXShadow, scaleYShadow);
        animatorSet.setDuration(1200);
        animatorSet.start();

        // setelah animasi selesai masuk ke WelcomeActivity
        new Handler().postDelayed(() -> {
            startActivity(new Intent(SplashActivity.this, WelcomeActivity.class));
            finish();
        }, 1500);
    }
}
```
## 2. Welcome Message

### Layout
**Code XML: `activity_welcome`**
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#62E0FD">

    <!-- Grup ikon lokasi + bendera -->
    <LinearLayout
        android:id="@+id/locationFlagGroup"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentTop="true"
        android:layout_alignParentEnd="true"
        android:layout_marginTop="30dp"
        android:layout_marginEnd="30dp"
        android:orientation="vertical"
        android:gravity="center_horizontal">

        <!-- Ikon lokasi -->

        <!-- Bendera -->
        <TextView
            android:id="@+id/namanegara"
            android:layout_width="80dp"
            android:layout_height="wrap_content"
            android:layout_centerInParent="true"
            android:layout_marginBottom="4dp"
            android:alpha="0"
            android:textColor="@android:color/black"
            android:textSize="30sp"
            android:textAlignment="center"
            android:textStyle="bold" />

        <ImageView
            android:id="@+id/flagImage"
            android:layout_width="60dp"
            android:layout_height="40dp"
            android:src="@drawable/flag_indonesia"
            android:alpha="0" />
    </LinearLayout>

    <!-- Teks di tengah layar -->
    <TextView
        android:id="@+id/welcomeText"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Detecting location..."
        android:textSize="40sp"
        android:textColor="@android:color/black"
        android:textStyle="bold"
        android:alpha="0" />

    <ImageView
        android:id="@+id/globeIcon"
        android:layout_width="150dp"
        android:layout_height="150dp"
        android:src="@drawable/ic_globe"
        android:layout_gravity="center"
        android:alpha="1"
        android:layout_centerInParent="true"
        android:layout_marginTop="40dp"/>

</RelativeLayout>

```

### Methode
**Java CLass: `WelcomeActivity`**
```java
package com.example.bmitracker;

import android.Manifest;
import android.content.Intent;
import android.content.pm.PackageManager;
import android.location.Address;
import android.location.Geocoder;
import android.location.Location;
import android.os.Bundle;
import android.os.Handler;
import android.util.Log;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;

import com.google.android.gms.location.FusedLocationProviderClient;
import com.google.android.gms.location.LocationCallback;
import com.google.android.gms.location.LocationRequest;
import com.google.android.gms.location.LocationResult;
import com.google.android.gms.location.LocationServices;

import java.io.IOException;
import java.util.List;
import java.util.Locale;

public class WelcomeActivity extends AppCompatActivity {

    private static final int LOCATION_PERMISSION_CODE = 100;
    private TextView welcomeText;
    private TextView NamaNegara;
    private ImageView flagImage;
    private FusedLocationProviderClient fusedLocationClient;
    private LocationCallback locationCallback;
    private ImageView globeIcon;
    private Animation fadeIn, fadeOut, flagGlow;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_welcome);
        globeIcon = findViewById(R.id.globeIcon);

        Animation zoomIn = AnimationUtils.loadAnimation(this, R.anim.zoom_in);

        fadeIn = AnimationUtils.loadAnimation(this, R.anim.fade_in);
        fadeOut = AnimationUtils.loadAnimation(this, R.anim.fade_out);
        flagGlow = AnimationUtils.loadAnimation(this, R.anim.flag_glow);


        globeIcon.startAnimation(fadeIn);
        globeIcon.startAnimation(zoomIn);

        NamaNegara = findViewById(R.id.namanegara);
        welcomeText = findViewById(R.id.welcomeText);
        flagImage = findViewById(R.id.flagImage);
        fusedLocationClient = LocationServices.getFusedLocationProviderClient(this);

        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                != PackageManager.PERMISSION_GRANTED) {
            ActivityCompat.requestPermissions(this,
                    new String[]{Manifest.permission.ACCESS_FINE_LOCATION},
                    LOCATION_PERMISSION_CODE);
        } else {
            startLocationUpdates();
        }
    }

    private void setAppLocale(String lang) {
        Locale locale = new Locale(lang);
        Locale.setDefault(locale);

        android.content.res.Configuration config = new android.content.res.Configuration();
        config.setLocale(locale);

        getBaseContext().getResources().updateConfiguration(
                config,
                getBaseContext().getResources().getDisplayMetrics()
        );
    }

    private void startLocationUpdates() {
        LocationRequest locationRequest = LocationRequest.create()
                .setInterval(2000)
                .setFastestInterval(1000)
                .setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);

        locationCallback = new LocationCallback() {
            @Override
            public void onLocationResult(@NonNull LocationResult locationResult) {
                if (locationResult == null) return;
                Location location = locationResult.getLastLocation();
                if (location != null) {
                    detectCountry(location.getLatitude(), location.getLongitude());
                    fusedLocationClient.removeLocationUpdates(locationCallback);
                }
            }
        };

        if (ActivityCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION)
                == PackageManager.PERMISSION_GRANTED) {
            fusedLocationClient.requestLocationUpdates(locationRequest, locationCallback, getMainLooper());
        }
    }

    private void detectCountry(double latitude, double longitude) {
        String countryCode = null;

        try {
            Geocoder geocoder = new Geocoder(this, Locale.getDefault());
            List<Address> addresses = geocoder.getFromLocation(latitude, longitude, 1);

            if (addresses != null && !addresses.isEmpty()) {
                countryCode = addresses.get(0).getCountryCode();
                Log.d("WelcomeActivity", "Detected country code: " + countryCode);
            } else {
                Log.w("WelcomeActivity", "Geocoder returned empty address list.");
            }
        } catch (IOException e) {
            Log.e("WelcomeActivity", "Geocoder failed: " + e.getMessage());
        }

        // Fallback jika countryCode null
        if (countryCode == null || countryCode.isEmpty()) {
            countryCode = Locale.getDefault().getCountry(); // fallback ke locale perangkat
            Log.d("WelcomeActivity", "Fallback to Locale country code: " + countryCode);
        }

        showWelcome(countryCode);
    }

    private void showWelcome(String countryCode) {
        globeIcon.clearAnimation();
        globeIcon.startAnimation(fadeOut);

        globeIcon.startAnimation(fadeOut);
        globeIcon.setVisibility(View.INVISIBLE);
        flagImage.setVisibility(View.VISIBLE);
        flagImage.startAnimation(fadeIn);
        flagImage.startAnimation(flagGlow);

        switch (countryCode) {
            case "ID":
                setAppLocale("id");
                flagImage.setImageResource(R.drawable.flag_indonesia);
                welcomeText.setText("Selamat Datang!");
                NamaNegara.setText("IDN");
                break;
            case "SA":
                setAppLocale("ar");
                flagImage.setImageResource(R.drawable.flag_saudi_arabia);
                welcomeText.setText("مرحبًا بك!");
                NamaNegara.setText("SAU");
                break;
            case "US":
                setAppLocale("en");
                flagImage.setImageResource(R.drawable.flag_usa);
                welcomeText.setText("Welcome!");
                NamaNegara.setText("USA");
                break;
            case "JP":
                setAppLocale("ja");
                flagImage.setImageResource(R.drawable.flag_japan);
                welcomeText.setText("ようこそ!");
                NamaNegara.setText("JPN");
                break;
            case "KR":
                setAppLocale("ko");
                flagImage.setImageResource(R.drawable.flag_south_korea);
                welcomeText.setText("환영합니다!");
                NamaNegara.setText("KOR");
                break;
            case "CN":
                setAppLocale("zh");
                flagImage.setImageResource(R.drawable.flag_china);
                welcomeText.setText("欢迎光临!");
                NamaNegara.setText("CHN");
                break;
            case "FR":
                setAppLocale("fr");
                flagImage.setImageResource(R.drawable.flag_france);
                welcomeText.setText("Bienvenue!");
                NamaNegara.setText("FRA");
                break;
            case "DE":
                setAppLocale("de");
                flagImage.setImageResource(R.drawable.flag_germany);
                welcomeText.setText("Willkommen!");
                NamaNegara.setText("DEU");
                break;
            case "ES":
                setAppLocale("es");
                flagImage.setImageResource(R.drawable.flag_spain);
                welcomeText.setText("¡Bienvenido!");
                NamaNegara.setText("ESP");
                break;
            case "PT":
                setAppLocale("pt");
                flagImage.setImageResource(R.drawable.flag_portugal);
                welcomeText.setText("Bem-vindo!");
                NamaNegara.setText("PRT");
                break;
            case "IT":
                setAppLocale("it");
                flagImage.setImageResource(R.drawable.flag_italy);
                welcomeText.setText("Benvenuto!");
                NamaNegara.setText("ITA");
                break;
            default:
                setAppLocale("id");
                flagImage.setImageResource(R.drawable.flag_indonesia);
                welcomeText.setText("Selamat Datang!");
                NamaNegara.setText("IDN");
                break;
        }

        animateWelcome();

        new Handler().postDelayed(() -> {
            Intent intent = new Intent(WelcomeActivity.this, HomeActivity.class);
            startActivity(intent);
            finish();
        }, 2500);
    }

    private void animateWelcome() {
        NamaNegara.setTranslationY(-50f);
        flagImage.setTranslationY(-30f);

        NamaNegara.animate().translationY(0).alpha(1f).setDuration(800).start();
        flagImage.animate().translationY(0).alpha(1f).setDuration(800).setStartDelay(200).start();
        welcomeText.animate().alpha(1f).setDuration(800).start();
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions,
                                           @NonNull int[] grantResults) {
        super.onRequestPermissionsResult(requestCode, permissions, grantResults);
        if (requestCode == LOCATION_PERMISSION_CODE &&
                grantResults.length > 0 &&
                grantResults[0] == PackageManager.PERMISSION_GRANTED) {
            startLocationUpdates();
        } else {
            // Jika izin ditolak, tetap lanjut dengan default
            showWelcome(Locale.getDefault().getCountry());
        }
    }
}
```


## 3. Activity Home

### Layout
**Code XML: `activity_home`**
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#f8f8f8">

    <!-- 🔝 Bar atas -->

    <!-- 🟦 Container besar -->
    <LinearLayout
        android:id="@+id/topBar"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:layout_alignParentTop="true"
        android:background="#62E0FD"
        android:elevation="4dp"
        android:gravity="center_vertical"
        android:orientation="horizontal"
        android:paddingStart="16dp">

        <ImageView
            android:id="@+id/iconHome"
            android:layout_width="35dp"
            android:layout_height="35dp"
            android:layout_marginEnd="8dp"
            android:src="@drawable/ic_home_inactive" />

        <TextView
            android:id="@+id/topBarTitle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/home_menu"
            android:textColor="#000000"
            android:textSize="40sp" />
    </LinearLayout>

    <!-- 🔘 Tombol utama -->
    <LinearLayout
        android:id="@+id/outerContainer"
        android:layout_width="400dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/topBar"
        android:layout_marginHorizontal="25dp"
        android:layout_marginTop="15dp"
        android:background="@drawable/bg_rounded_white"
        android:elevation="4dp"
        android:gravity="center_horizontal"
        android:orientation="vertical"
        android:padding="24dp">

        <!-- 🟩 Container kecil -->
        <LinearLayout
            android:id="@+id/innerContainer"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_rounded_white1"
            android:elevation="2dp"
            android:gravity="center"
            android:paddingHorizontal="30dp"
            android:paddingVertical="8dp">

            <TextView
                android:id="@+id/titleText"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/app_name"
                android:textColor="#000000"
                android:textSize="40sp" />
        </LinearLayout>

        <!-- 📝 Subjudul -->
        <TextView
            android:id="@+id/subtitleText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="12dp"
            android:text="@string/subtitle"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/mainButtons"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@id/outerContainer"
        android:layout_marginHorizontal="32dp"
        android:layout_marginTop="30dp"
        android:gravity="center_horizontal"
        android:orientation="vertical">

        <Button
            android:id="@+id/btnHitung"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="16dp"
            android:backgroundTint="#00AAFF"
            android:elevation="5dp"
            android:layout_marginHorizontal="50dp"
            android:text="@string/button_home1"
            android:textSize="16dp"
            android:textColor="#000000"/>

        <Button
            android:id="@+id/btnRiwayat"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="16dp"
            android:backgroundTint="#00AAFF"
            android:elevation="5dp"
            android:text="@string/button_home2"
            android:layout_marginHorizontal="50dp"
            android:textSize="16dp"
            android:textColor="#000000"/>

        <Button
            android:id="@+id/btnTentang"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:backgroundTint="#00AAFF"
            android:elevation="5dp"
            android:text="@string/button_home3"
            android:layout_marginHorizontal="50dp"
            android:textSize="16dp"
            android:textColor="#000000"/>
    </LinearLayout>

    <!-- 📱 Nav-bar bawah -->
    <LinearLayout
        android:id="@+id/navBar"
        android:layout_width="match_parent"
        android:layout_height="72dp"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:background="#62E0FD"
        android:elevation="8dp">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navHomeActive"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_home_active"
                android:elevation="8dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navFormulir1"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_plus_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navRiwayat1"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_calendar_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navTentang1"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_info_inactive"
                android:elevation="5dp"/>
        </LinearLayout>
    </LinearLayout>
</RelativeLayout>
```

### Methode
**Java CLass: `HomeActivity`**
```java
package com.example.bmitracker;

import android.content.Intent;
import android.os.Bundle;
import android.widget.Button;
import android.widget.ImageView;
import androidx.appcompat.app.AppCompatActivity;

public class HomeActivity extends AppCompatActivity {

    // Durasi animasi yang ideal adalah antara 300ms hingga 500ms
    private final int ANIM_DURATION = 300;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_home);

        // Inisialisasi tombol dan ikon
        Button btnHitung = findViewById(R.id.btnHitung);
        Button btnRiwayat = findViewById(R.id.btnRiwayat);
        Button btnTentang = findViewById(R.id.btnTentang);

        ImageView navHome = findViewById(R.id.navHomeActive);
        ImageView navFormulir = findViewById(R.id.navFormulir1);
        ImageView navRiwayat = findViewById(R.id.navRiwayat1);
        ImageView navTentang = findViewById(R.id.navTentang1);

        // Navigasi tombol
        btnHitung.setOnClickListener(v -> {
            startActivity(new Intent(this, MainActivity.class));
            // Tambahkan animasi: [Halaman Masuk], [Halaman Keluar]
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        btnRiwayat.setOnClickListener(v -> {
            startActivity(new Intent(this, RiwayatActivity.class));
            // Tambahkan animasi: [Halaman Masuk], [Halaman Keluar]
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        btnTentang.setOnClickListener(v -> {
            startActivity(new Intent(this, TentangActivity.class));
            // Tambahkan animasi: [Halaman Masuk], [Halaman Keluar]
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        // Navigasi ikon bawah
        navHome.setOnClickListener(v -> recreate());

        navFormulir.setOnClickListener(v -> {
            startActivity(new Intent(this, MainActivity.class));
            // Tambahkan animasi: [Halaman Masuk], [Halaman Keluar]
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        navRiwayat.setOnClickListener(v -> {
            startActivity(new Intent(this, RiwayatActivity.class));
            // Tambahkan animasi: [Halaman Masuk], [Halaman Keluar]
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        navTentang.setOnClickListener(v -> {
            startActivity(new Intent(this, TentangActivity.class));
            // Tambahkan animasi: [Halaman Masuk], [Halaman Keluar]
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });
    }
}
```



## 4. Activity Main

### Layout
**Code XML: `activity_main`**
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#f8f8f8">

    <LinearLayout
        android:id="@+id/topBar"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:background="#62E0FD"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:paddingStart="16dp"
        android:elevation="4dp"
        android:layout_alignParentTop="true">

        <ImageView
            android:id="@+id/iconArrowHitung"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:src="@drawable/ic_arrow"
            android:layout_marginEnd="8dp" />

        <TextView
            android:id="@+id/topBarTitle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/topbar_main"
            android:textSize="36sp"
            android:textColor="#000000" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/outerContainer"
        android:layout_width="400dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/topBar"
        android:layout_marginHorizontal="25dp"
        android:layout_marginTop="15dp"
        android:background="@drawable/bg_rounded_white"
        android:elevation="4dp"
        android:gravity="center_horizontal"
        android:orientation="vertical"
        android:padding="24dp">

        <LinearLayout
            android:id="@+id/innerContainer"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_rounded_white1"
            android:elevation="2dp"
            android:gravity="center"
            android:paddingHorizontal="30dp"
            android:paddingVertical="8dp">

            <TextView
                android:id="@+id/titleText"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/app_name"
                android:textColor="#000000"
                android:textSize="40sp" />
        </LinearLayout>

        <TextView
            android:id="@+id/subtitleText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="12dp"
            android:text="@string/subtitle"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>


    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:paddingHorizontal="50dp"
        android:layout_marginTop="10dp"
        android:layout_below="@+id/outerContainer"
        android:layout_above="@+id/navBar">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/forminput1"
            android:textColor="#000000"
            android:layout_marginStart="16dp"
            android:textSize="16sp" />

        <EditText
            android:id="@+id/inputTinggi"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_border_gray" android:elevation="2dp"
            android:layout_marginHorizontal="16dp"
            android:hint="@string/hint1"
            android:inputType="numberDecimal"
            android:padding="12dp"
            android:textColor="#000000" />

        <TextView
            android:id="@+id/errorTinggi"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginStart="16dp"
            android:layout_marginEnd="16dp"
            android:textColor="#FF0000"
            android:textSize="12sp"
            android:visibility="gone"
            android:text="harus di isi!" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:text="@string/forminput2"
            android:textColor="#000000"
            android:layout_marginStart="16dp"
            android:textSize="16sp" />

        <EditText
            android:id="@+id/inputBerat"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_border_gray" android:elevation="2dp"
            android:layout_marginHorizontal="16dp"
            android:hint="@string/hint2"
            android:inputType="numberDecimal"
            android:padding="12dp"
            android:textColor="#000000" />

        <TextView
            android:id="@+id/errorBerat"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginStart="16dp"
            android:layout_marginEnd="16dp"
            android:textColor="#FF0000"
            android:textSize="12sp"
            android:visibility="gone"
            android:text="harus di isi!" />

        <Button
            android:id="@+id/btnHitung"
            android:layout_width="160dp"
            android:layout_height="wrap_content"
            android:layout_gravity="center_horizontal"
            android:layout_marginTop="24dp"
            android:layout_marginBottom="24dp"
            android:backgroundTint="#00aaff"
            android:elevation="4dp"
            android:textSize="16sp"
            android:text="@string/buttonhitung"
            android:textColor="#000000"
            android:textStyle="bold" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/navBar"
        android:layout_width="match_parent"
        android:layout_height="72dp"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:background="#62E0FD"
        android:elevation="8dp">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navHome2"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_home_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navFormulirActive"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_plus_active"
                android:elevation="8dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navRiwayat2"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_calendar_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navTentang2"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_info_inactive"
                android:elevation="5dp"/>
        </LinearLayout>
    </LinearLayout>
</RelativeLayout>
```

### Methode
**Java CLass: `MainActivity`**
```java
package com.example.bmitracker;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;

import org.json.JSONArray;
import org.json.JSONObject;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Locale;

public class MainActivity extends AppCompatActivity {

    EditText inputTinggi, inputBerat;
    TextView errorTinggi, errorBerat;
    Button btnHitung;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 🔗 Navigasi bawah
        ImageView arrowFormulir = findViewById(R.id.iconArrowHitung);
        ImageView navHome = findViewById(R.id.navHome2);
        ImageView navFormulir = findViewById(R.id.navFormulirActive);
        ImageView navRiwayat = findViewById(R.id.navRiwayat2);
        ImageView navTentang = findViewById(R.id.navTentang2);

        // --- TAMBAH ANIMASI SAAT PINDAH ---

        navHome.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            // Transisi BALIK (seolah-olah kembali)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navFormulir.setOnClickListener(v -> recreate());

        navRiwayat.setOnClickListener(v -> {
            startActivity(new Intent(this, RiwayatActivity.class));
            // Transisi NORMAL (ke halaman baru)
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        navTentang.setOnClickListener(v -> {
            startActivity(new Intent(this, TentangActivity.class));
            // Transisi NORMAL (ke halaman baru)
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        arrowFormulir.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            // Transisi BALIK (seolah-olah kembali)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });


        // 📝 Input
        inputTinggi = findViewById(R.id.inputTinggi);
        inputBerat = findViewById(R.id.inputBerat);
        errorTinggi = findViewById(R.id.errorTinggi);
        errorBerat = findViewById(R.id.errorBerat);
        btnHitung = findViewById(R.id.btnHitung);

        btnHitung.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (validateInputs()) {
                    hitungBmiDanSimpan();
                }
            }
        });

        // Listener fokus untuk menghapus pesan error
        inputTinggi.setOnFocusChangeListener((v, hasFocus) -> {
            if (hasFocus) {
                inputTinggi.setBackgroundResource(R.drawable.bg_border_gray);
                errorTinggi.setVisibility(View.GONE);
            }
        });
        inputBerat.setOnFocusChangeListener((v, hasFocus) -> {
            if (hasFocus) {
                inputBerat.setBackgroundResource(R.drawable.bg_border_gray);
                errorBerat.setVisibility(View.GONE);
            }
        });
    }

    /**
     * Override finish() untuk menerapkan animasi saat Activity ini ditutup
     * (misal: tombol back ditekan).
     */
    @Override
    public void finish() {
        super.finish();
        // Transisi BALIK (slide keluar ke kanan, halaman lama masuk dari kiri)
        overridePendingTransition(R.anim.slide_out_left, R.anim.slide_out_right);
    }

    private boolean validateInputs() {
        boolean isValid = true;
        // ... (Kode validasi yang sama)
        String tinggiStr = inputTinggi.getText().toString().trim();
        String beratStr = inputBerat.getText().toString().trim();

        // 1. Validasi Tinggi Badan
        if (tinggiStr.isEmpty()) {
            inputTinggi.setBackgroundResource(R.drawable.bg_border_red);
            errorTinggi.setVisibility(View.VISIBLE);
            isValid = false;
        } else {
            inputTinggi.setBackgroundResource(R.drawable.bg_border_gray);
            errorTinggi.setVisibility(View.GONE);
        }

        // 2. Validasi Berat Badan
        if (beratStr.isEmpty()) {
            inputBerat.setBackgroundResource(R.drawable.bg_border_red);
            errorBerat.setVisibility(View.VISIBLE);
            isValid = false;
        } else {
            inputBerat.setBackgroundResource(R.drawable.bg_border_gray);
            errorBerat.setVisibility(View.GONE);
        }

        return isValid;
    }

    private void hitungBmiDanSimpan() {
        String tinggiStr = inputTinggi.getText().toString();
        String beratStr = inputBerat.getText().toString();

        float tinggi = Float.parseFloat(tinggiStr) / 100; // cm ke meter
        float berat = Float.parseFloat(beratStr);
        float bmi = berat / (tinggi * tinggi);

        String bmiValue = String.format(Locale.getDefault(), "%.1f", bmi);
        String bmiStatus = getStatusFromBMI(bmi);
        String bmiMessage = getMessageFromBMI(bmi);

        // 💾 Simpan ke SharedPreferences
        SharedPreferences prefs = getSharedPreferences("BMI_PREFS", MODE_PRIVATE);
        SharedPreferences.Editor editor = prefs.edit();

        String existingData = prefs.getString("riwayat", "[]");
        JSONArray riwayatArray;

        try {
            riwayatArray = new JSONArray(existingData);
        } catch (Exception e) {
            riwayatArray = new JSONArray();
        }

        JSONObject newEntry = new JSONObject();
        try {
            newEntry.put("tanggal", getTodayDate());
            newEntry.put("nilai", bmiValue);
            newEntry.put("status", bmiStatus);
            newEntry.put("keterangan", bmiMessage);
            riwayatArray.put(newEntry);
        } catch (Exception e) {
            e.printStackTrace();
        }

        editor.putString("riwayat", riwayatArray.toString());
        editor.apply();

        // 🚀 Navigasi ke ResultActivity
        Intent intent = new Intent(MainActivity.this, ResultActivity.class);
        intent.putExtra("bmi", bmi);
        startActivity(intent);
        // Transisi NORMAL (ke halaman baru)
        overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
    }

    private String getTodayDate() {
        SimpleDateFormat sdf = new SimpleDateFormat("dd/MM/yyyy", Locale.getDefault());
        return sdf.format(new Date());
    }

    private String getStatusFromBMI(float bmi) {
        if (bmi < 18.5) return "Kurus";
        else if (bmi < 25) return "Normal";
        else if (bmi < 30) return "Gemuk";
        else return "Obesitas";
    }

    private String getMessageFromBMI(float bmi) {
        if (bmi < 18.5) return "Berat badan anda kurang";
        else if (bmi < 25) return "Berat badan anda ideal";
        else if (bmi < 30) return "Berat badan anda berlebih";
        else return "Berat badan anda obesitas";
    }
}
```


## 5. Activity Result

### Layout
**Code XML: `activity_result`**
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#f8f8f8">

    <!-- 🔙 TOP BAR -->


    <LinearLayout
        android:id="@+id/topBar"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:background="#62E0FD"
        android:elevation="4dp"
        android:gravity="center_vertical"
        android:orientation="horizontal"
        android:paddingStart="16dp">

        <ImageView
            android:id="@+id/iconArrowHitung"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:layout_marginEnd="8dp"
            android:src="@drawable/ic_arrow" />

        <TextView
            android:id="@+id/topBarTitle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/topbar_main"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/outerContainer"
        android:layout_width="400dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/topBar"
        android:layout_marginHorizontal="25dp"
        android:layout_marginTop="15dp"
        android:background="@drawable/bg_rounded_white"
        android:elevation="4dp"
        android:gravity="center_horizontal"
        android:orientation="vertical"
        android:padding="24dp">

        <!-- 🟩 Container kecil -->
        <LinearLayout
            android:id="@+id/innerContainer"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_rounded_white1"
            android:elevation="2dp"
            android:gravity="center"
            android:paddingHorizontal="30dp"
            android:paddingVertical="8dp">

            <TextView
                android:id="@+id/titleText"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/app_name"
                android:textColor="#000000"
                android:textSize="40sp" />
        </LinearLayout>

        <!-- 📝 Subjudul -->
        <TextView
            android:id="@+id/subtitleText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="12dp"
            android:text="@string/subtitle"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>


    <!-- 🔲 CARD HASIL BMI -->
    <TextView
        android:id="@+id/Hasilteks"
        android:layout_width="wrap_content"
        android:layout_height="35dp"
        android:layout_below="@+id/outerContainer"
        android:layout_centerHorizontal="true"
        android:layout_marginTop="26dp"
        android:text="@string/hasilteks"
        android:textColor="#000000"
        android:textSize="30sp"
        android:textStyle="bold" />

    <LinearLayout
        android:id="@+id/resultCard"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/Hasilteks"
        android:layout_marginTop="5dp"
        android:orientation="vertical"
        android:layout_centerHorizontal="true"
        android:background="@drawable/bg_rounded_white1"
        android:elevation="5dp"
        android:padding="20dp"
        android:gravity="center_horizontal">

        <TextView
            android:id="@+id/bmiValue"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="22.4"
            android:textSize="30sp"
            android:textStyle="bold"
            android:gravity="center"
            android:layout_marginBottom="8dp"/>

        <TextView
            android:id="@+id/bmiCategory"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Normal"
            android:textSize="18sp"
            android:layout_marginBottom="10dp" />


        <TextView
            android:id="@+id/bmiDescription"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Berat badan anda ideal"
            android:textColor="#666666"
            android:textSize="14sp"/>
    </LinearLayout>


    <!-- 🔘 BUTTON -->
    <Button
        android:id="@+id/btnKembali"
        android:layout_width="160dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/resultCard"
        android:layout_marginTop="25dp"
        android:layout_centerHorizontal="true"
        android:backgroundTint="#00aaff"
        android:text="@string/buttonhitungulang"
        android:textColor="#000"
        android:textStyle="bold"
        android:elevation="4dp" />

    <LinearLayout
        android:id="@+id/navBar"
        android:layout_width="match_parent"
        android:layout_height="72dp"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:background="#62E0FD"
        android:elevation="8dp">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navHome5"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_home_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navFormulirActive1"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_plus_active"
                android:elevation="8dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navRiwayat5"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_calendar_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navTentang5"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_info_inactive"
                android:elevation="5dp"/>
        </LinearLayout>
    </LinearLayout>
</RelativeLayout>
```

### Methode
**Java CLass: `ResultActivity`**
```java
package com.example.bmitracker;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;
import androidx.appcompat.app.AppCompatActivity;

public class ResultActivity extends AppCompatActivity {

    TextView bmiValue, bmiCategory, bmiDescription;
    Button btnKembali;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_result);

        ImageView arrowFormulir = findViewById(R.id.iconArrowHitung);
        ImageView navHome = findViewById(R.id.navHome5);
        ImageView navFormulir = findViewById(R.id.navFormulirActive1);
        ImageView navRiwayat = findViewById(R.id.navRiwayat5);
        ImageView navTentang = findViewById(R.id.navTentang5);

        // --- Navigasi dengan Animasi ---

        navHome.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            // Transisi BALIK (kembali ke Home)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        // navFormulir (recreate) tidak memerlukan animasi

        navRiwayat.setOnClickListener(v -> {
            startActivity(new Intent(this, RiwayatActivity.class));
            // Transisi NORMAL (ke halaman baru)
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        navTentang.setOnClickListener(v -> {
            startActivity(new Intent(this, TentangActivity.class));
            // Transisi NORMAL (ke halaman baru)
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        arrowFormulir.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            // Transisi BALIK (kembali ke Home)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        // --- Inisialisasi UI dan Logika BMI ---

        bmiValue = findViewById(R.id.bmiValue);
        bmiCategory = findViewById(R.id.bmiCategory);
        bmiDescription = findViewById(R.id.bmiDescription);
        btnKembali = findViewById(R.id.btnKembali);

        // Ambil data dari Intent
        Intent intent = getIntent();
        float bmi = intent.getFloatExtra("bmi", 0f);

        // Tampilkan nilai BMI
        bmiValue.setText(String.format("%.1f", bmi));

        // Tentukan kategori dan deskripsi
        String kategori, deskripsi;
        if (bmi < 18.5) {
            kategori = getString(R.string.bmi_underweight);
            deskripsi = getString(R.string.bmi_underweight_desc);
        } else if (bmi < 25) {
            kategori = getString(R.string.bmi_normal);
            deskripsi = getString(R.string.bmi_normal_desc);
        } else if (bmi < 30) {
            kategori = getString(R.string.bmi_overweight);
            deskripsi = getString(R.string.bmi_overweight_desc);
        } else {
            kategori = getString(R.string.bmi_obesity);
            deskripsi = getString(R.string.bmi_obesity_desc);
        }


        bmiCategory.setText(kategori);
        bmiDescription.setText(deskripsi);

        // Tombol kembali ke MainActivity
        btnKembali.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent kembali = new Intent(ResultActivity.this, MainActivity.class);
                startActivity(kembali);
                finish();
                // Transisi BALIK saat kembali ke MainActivity
                overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
            }
        });
    }

    /**
     * Override finish() untuk menerapkan animasi saat tombol back ditekan
     * atau Activity ini ditutup.
     */
    @Override
    public void finish() {
        super.finish();
        // Transisi BALIK (slide keluar ke kanan)
        overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
    }
}
```


## 6. Activity Riwayat

### Layout
**Code XML: `activity_riwayat`**
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#f8f8f8">

    <LinearLayout
        android:id="@+id/topBar"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:background="#62E0FD"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:paddingStart="16dp"
        android:elevation="4dp"
        android:layout_alignParentTop="true">

        <ImageView
            android:id="@+id/iconArrowRiwayat"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:src="@drawable/ic_arrow"
            android:layout_marginEnd="8dp" />

        <TextView
            android:id="@+id/topBarTitle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/topbar_riwayat"
            android:textSize="36sp"
            android:textColor="#000000" />
    </LinearLayout>

    <LinearLayout
        android:id="@+id/outerContainer"
        android:layout_width="400dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/topBar"
        android:layout_marginHorizontal="25dp"
        android:layout_marginTop="15dp"
        android:background="@drawable/bg_rounded_white"
        android:elevation="4dp"
        android:gravity="center_horizontal"
        android:orientation="vertical"
        android:padding="24dp">

        <LinearLayout
            android:id="@+id/innerContainer"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_rounded_white1"
            android:elevation="2dp"
            android:gravity="center"
            android:paddingHorizontal="30dp"
            android:paddingVertical="8dp">

            <TextView
                android:id="@+id/titleText"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/app_name"
                android:textColor="#000000"
                android:textSize="40sp" />
        </LinearLayout>

        <TextView
            android:id="@+id/subtitleText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="12dp"
            android:text="@string/subtitle"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@+id/outerContainer"
        android:layout_above="@+id/navBar"
        android:paddingTop="10dp">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <TextView
                android:id="@+id/TeksRiwayat"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginBottom="10dp"
                android:text="@string/Teksriwayat"
                android:textColor="#000000"
                android:textSize="24sp"
                android:textStyle="bold"
                android:layout_marginStart="25dp" />

            <LinearLayout
                android:id="@+id/listRiwayat"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="vertical"
                android:layout_marginHorizontal="25dp"
                android:paddingBottom="10dp" />
        </LinearLayout>
    </ScrollView>

    <LinearLayout
        android:id="@+id/navBar"
        android:layout_width="match_parent"
        android:layout_height="72dp"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:background="#62E0FD"
        android:elevation="8dp">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navHome3"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_home_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navFormulir3"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_plus_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navRiwayatActive"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_calendar_active"
                android:elevation="8dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navTentang3"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_info_inactive"
                android:elevation="5dp"/>
        </LinearLayout>
    </LinearLayout>
</RelativeLayout>
```

### Methode
**Java CLass: `RiwayatActivity`**
```java
package com.example.bmitracker;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;
import android.widget.LinearLayout;
import android.widget.RelativeLayout;
import android.widget.TextView;
import android.widget.Toast;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.content.ContextCompat;

import org.json.JSONArray;
import org.json.JSONObject;

public class RiwayatActivity extends AppCompatActivity {

    private static final String PREFS_NAME = "BMI_PREFS";
    private static final String RIWAYAT_KEY = "riwayat";

    private LinearLayout listContainer;
    private SharedPreferences prefs;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_riwayat);

        prefs = getSharedPreferences(PREFS_NAME, MODE_PRIVATE);
        listContainer = findViewById(R.id.listRiwayat);

        ImageView arrowRiwayat = findViewById(R.id.iconArrowRiwayat);
        ImageView navHome = findViewById(R.id.navHome3);
        ImageView navFormulir = findViewById(R.id.navFormulir3);
        ImageView navRiwayat = findViewById(R.id.navRiwayatActive);
        ImageView navTentang = findViewById(R.id.navTentang3);

        arrowRiwayat.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navHome.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navFormulir.setOnClickListener(v -> {
            startActivity(new Intent(this, MainActivity.class));
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navRiwayat.setOnClickListener(v -> recreate());

        navTentang.setOnClickListener(v -> {
            startActivity(new Intent(this, TentangActivity.class));
            overridePendingTransition(R.anim.slide_in_right, R.anim.slide_out_left);
        });

        loadRiwayat();
    }

    @Override
    public void finish() {
        super.finish();
        overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
    }

    private void loadRiwayat() {
        String data = prefs.getString(RIWAYAT_KEY, "[]");

        try {
            JSONArray array = new JSONArray(data);
            listContainer.removeAllViews();

            for (int i = array.length() - 1; i >= 0; i--) {
                JSONObject item = array.getJSONObject(i);

                // Perbaiki data lama kalau masih teks biasa
                fixLegacyItem(item);

                RelativeLayout itemLayout = createRiwayatItemView(item, i);
                listContainer.addView(itemLayout);
            }

        } catch (Exception e) {
            e.printStackTrace();
            Toast.makeText(this, "Gagal memuat riwayat", Toast.LENGTH_SHORT).show();
        }
    }

    /**
     * Mengonversi data lama ke format multibahasa jika masih berisi teks.
     */
    private void fixLegacyItem(JSONObject item) {
        try {
            // Jika sudah menggunakan kode → tidak perlu diperbaiki
            if (item.has("category_code")) return;

            String status = item.getString("status");
            String description = item.getString("keterangan");

            String categoryCode;
            String descriptionCode;

            if (status.equalsIgnoreCase("Kurus")) {
                categoryCode = "UNDERWEIGHT";
                descriptionCode = "UNDERWEIGHT";
            } else if (status.equalsIgnoreCase("Normal")) {
                categoryCode = "NORMAL";
                descriptionCode = "NORMAL";
            } else if (status.equalsIgnoreCase("Gemuk")) {
                categoryCode = "OVERWEIGHT";
                descriptionCode = "OVERWEIGHT";
            } else {
                categoryCode = "OBESE";
                descriptionCode = "OBESE";
            }

            item.put("category_code", categoryCode);
            item.put("description_code", descriptionCode);

        } catch (Exception ignore) {
        }
    }

    /**
     * Membuat 1 baris item riwayat
     */
    private RelativeLayout createRiwayatItemView(JSONObject item, int indexToDelete) throws Exception {

        String tanggal = item.getString("tanggal");
        String nilai = item.getString("nilai");

        String categoryCode = item.getString("category_code");
        String descriptionCode = item.getString("description_code");

        // Ambil string dari resources sesuai bahasa
        String status = getCategoryText(categoryCode);
        String keterangan = getDescriptionText(descriptionCode);

        RelativeLayout itemLayout = new RelativeLayout(this);
        RelativeLayout.LayoutParams params = new RelativeLayout.LayoutParams(
                RelativeLayout.LayoutParams.MATCH_PARENT,
                RelativeLayout.LayoutParams.WRAP_CONTENT
        );
        params.setMargins(0, 0, 0, 16);
        itemLayout.setLayoutParams(params);
        itemLayout.setPadding(24, 24, 24, 24);
        itemLayout.setBackgroundResource(R.drawable.bg_rounded_white);

        // Teks
        TextView tv = new TextView(this);
        tv.setId(View.generateViewId());
        tv.setText(tanggal + "\n" + nilai + "  " + status + "\n" + keterangan);
        tv.setTextSize(14);
        tv.setTextColor(ContextCompat.getColor(this, android.R.color.black));

        RelativeLayout.LayoutParams tvParams = new RelativeLayout.LayoutParams(
                RelativeLayout.LayoutParams.WRAP_CONTENT,
                RelativeLayout.LayoutParams.WRAP_CONTENT
        );
        tvParams.addRule(RelativeLayout.ALIGN_PARENT_START);
        tv.setLayoutParams(tvParams);

        itemLayout.addView(tv);

        // Icon delete
        ImageView deleteIcon = new ImageView(this);
        deleteIcon.setId(View.generateViewId());
        deleteIcon.setImageResource(android.R.drawable.ic_menu_delete);

        RelativeLayout.LayoutParams iconParams = new RelativeLayout.LayoutParams(60, 60);
        iconParams.addRule(RelativeLayout.ALIGN_PARENT_END);
        iconParams.addRule(RelativeLayout.CENTER_VERTICAL);
        deleteIcon.setLayoutParams(iconParams);

        deleteIcon.setOnClickListener(v -> deleteRiwayatItem(indexToDelete));

        itemLayout.addView(deleteIcon);

        return itemLayout;
    }

    private String getCategoryText(String code) {
        switch (code) {
            case "UNDERWEIGHT":
                return getString(R.string.bmi_underweight);
            case "NORMAL":
                return getString(R.string.bmi_normal);
            case "OVERWEIGHT":
                return getString(R.string.bmi_overweight);
            default:
                return getString(R.string.bmi_obesity);
        }
    }

    private String getDescriptionText(String code) {
        switch (code) {
            case "UNDERWEIGHT":
                return getString(R.string.bmi_underweight_desc);
            case "NORMAL":
                return getString(R.string.bmi_normal_desc);
            case "OVERWEIGHT":
                return getString(R.string.bmi_overweight_desc);
            default:
                return getString(R.string.bmi_obesity_desc);
        }
    }

    private void deleteRiwayatItem(int index) {
        try {
            String data = prefs.getString(RIWAYAT_KEY, "[]");
            JSONArray array = new JSONArray(data);

            JSONArray newArray = new JSONArray();
            for (int i = 0; i < array.length(); i++) {
                if (i != index) newArray.put(array.getJSONObject(i));
            }

            prefs.edit().putString(RIWAYAT_KEY, newArray.toString()).apply();
            recreate();

        } catch (Exception e) {
            e.printStackTrace();
            Toast.makeText(this, "Gagal menghapus", Toast.LENGTH_SHORT).show();
        }
    }
}

```



## 7. Activity Tentang Aplikasi

### Layout
**Code XML: `activity_tentang`**
```xml
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="#f8f8f8">

    <!-- 🔝 Bar atas -->
    <LinearLayout
        android:id="@+id/topBar"
        android:layout_width="match_parent"
        android:layout_height="70dp"
        android:background="#62E0FD"
        android:orientation="horizontal"
        android:gravity="center_vertical"
        android:paddingStart="16dp"
        android:elevation="4dp"
        android:layout_alignParentTop="true">

        <ImageView
            android:id="@+id/iconArrowTentang"
            android:layout_width="40dp"
            android:layout_height="40dp"
            android:src="@drawable/ic_arrow"
            android:layout_marginEnd="8dp" />

        <TextView
            android:id="@+id/topBarTitle"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/topbar_tentang"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>

    <!-- 🟦 Container besar -->
    <LinearLayout
        android:id="@+id/outerContainer"
        android:layout_width="400dp"
        android:layout_height="wrap_content"
        android:layout_below="@id/topBar"
        android:layout_marginHorizontal="25dp"
        android:layout_marginTop="15dp"
        android:background="@drawable/bg_rounded_white"
        android:elevation="4dp"
        android:gravity="center_horizontal"
        android:orientation="vertical"
        android:padding="24dp">

        <!-- 🟩 Container kecil -->
        <LinearLayout
            android:id="@+id/innerContainer"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="@drawable/bg_rounded_white1"
            android:elevation="2dp"
            android:gravity="center"
            android:paddingHorizontal="30dp"
            android:paddingVertical="8dp">

            <TextView
                android:id="@+id/titleText"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/app_name"
                android:textColor="#000000"
                android:textSize="40sp" />
        </LinearLayout>

        <!-- 📝 Subjudul -->
        <TextView
            android:id="@+id/subtitleText"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="12dp"
            android:text="@string/subtitle"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="36sp" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@+id/outerContainer"
        android:layout_marginTop="10dp"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginBottom="10dp"
            android:text="@string/Tekstentang"
            android:textColor="#000000"
            android:textSize="22sp"
            android:textStyle="bold"
            android:layout_marginStart="25dp"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_marginHorizontal="25dp"
            android:lineSpacingExtra="6dp"
            android:text="@string/desc_app"
            android:textAlignment="center"
            android:textColor="#000000"
            android:textSize="20sp" />
    </LinearLayout>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/penulis"
        android:textSize="10sp"
        android:layout_alignParentBottom="true"
        android:layout_alignParentStart="true"
        android:layout_marginBottom="75dp"
        android:layout_marginLeft="5dp"
        android:textColor="#000000" />

    <!-- 📱 Nav-bar bawah -->
    <LinearLayout
        android:id="@+id/navBar"
        android:layout_width="match_parent"
        android:layout_height="72dp"
        android:layout_alignParentBottom="true"
        android:orientation="horizontal"
        android:background="#62E0FD"
        android:elevation="8dp">

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navHome4"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_home_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navFormulir4"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_plus_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navRiwayat4"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_calendar_inactive"
                android:elevation="5dp"/>
        </LinearLayout>

        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_weight="1"
            android:gravity="center">

            <ImageView
                android:id="@+id/navTentangActive"
                android:layout_width="35dp"
                android:layout_height="35dp"
                android:src="@drawable/ic_info_active"
                android:elevation="8dp"/>
        </LinearLayout>
    </LinearLayout>
</RelativeLayout>
```

### Methode
**Java CLass: `TentangActivity`**
```java
package com.example.bmitracker;

import android.content.Intent;
import android.os.Bundle;
import android.widget.ImageView;

import androidx.appcompat.app.AppCompatActivity;

public class TentangActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_tentang);

        ImageView arrowTentang = findViewById(R.id.iconArrowTentang);
        ImageView navHome = findViewById(R.id.navHome4);
        ImageView navFormulir = findViewById(R.id.navFormulir4);
        ImageView navRiwayat = findViewById(R.id.navRiwayat4);
        ImageView navTentang = findViewById(R.id.navTentangActive);

        // --- Navigasi dengan Animasi ---

        navHome.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            // Transisi BALIK (kembali ke Home)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navFormulir.setOnClickListener(v -> {
            startActivity(new Intent(this, MainActivity.class));
            // Transisi BALIK (kembali ke Formulir)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navRiwayat.setOnClickListener(v -> {
            startActivity(new Intent(this, RiwayatActivity.class));
            // Transisi BALIK (kembali ke Riwayat)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

        navTentang.setOnClickListener(v -> recreate());

        arrowTentang.setOnClickListener(v -> {
            startActivity(new Intent(this, HomeActivity.class));
            // Transisi BALIK (kembali ke Home)
            overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
        });

    }

    /**
     * Override finish() untuk menerapkan animasi saat tombol back ditekan
     * atau Activity ini ditutup.
     */
    @Override
    public void finish() {
        super.finish();
        // Transisi BALIK (slide keluar ke kanan)
        overridePendingTransition(R.anim.slide_in_left, R.anim.slide_out_right);
    }
}
```


