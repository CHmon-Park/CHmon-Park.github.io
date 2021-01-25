---
title: "Orientation Event"
excerpt: "Ways to make Activity proper in accordance with display orientation"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
  - event
  - orientation
  - savedInstanceState
  - configChanges
  - onConfigurationChanged
last_modified_at: 2021-01-21T18:47:00
---
<!--more-->

<br>

## 단말 방향 전환시 이벤트 처리

<img src="/images/2021-01-21-orientation.png" class="align-center" alt="">
<img src="/images/2021-01-21-orientation_ex02.png" class="align-center" alt="">

  * 단말의 방향이 바뀔 때 가로와 세로 화면의 비율에 따라 화면이 다시 보이게 된다. 즉, XMl 레이아웃이 다르게 보여야 하며, 이 때 액티비티는 메모리에서 없어졌다가 다시 만들어진다. 이에 따라 세로 방향의 XML 레이아웃과 가로 방향 XML 레이아웃이 따로 존재해야 한다.
  * 가로 방향의 XML 레이아웃은 /res/ 경로에 'layout-land'라는 폴더 안에 위치해야 한다.

**'layout-land' 폴더 만들 때**: 처음 layout-land 폴더를 만들 경우 아직 안드로이드와 관계가 없는 폴더이기에 프로젝트에는 보이지 않는다. 따라서 프로젝트에 띄울 파일을 'Project'로 지정해야 한다. 
{: .notice--info}

```java
<!--[MainActivity.java]-->

package com.example.orientation;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    String name;
    EditText editText;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        showToast("onCreate 호출됨.");

        editText = findViewById(R.id.editTextTextPersonName);

        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener(){

            @Override
            public void onClick(View v) {
                name = editText.getText().toString();
                showToast("입력된 값을 변수에 저장했습니다 : " + name);
            }
        });

        if (savedInstanceState != null) {
            name = savedInstanceState.getString("name");
            showToast("값을 복원했습니다 : " + name);
        }
    }

    @Override
    protected void onStart() {
        super.onStart();

        showToast("onStart 호출됨.");
    }

    @Override
    protected void onStop() {
        super.onStop();

        showToast("onStop 호출됨.");
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();

        showToast("onDestroy 호출됨.");
    }

    @Override
    protected void onSaveInstanceState(@NonNull Bundle outState) {
        super.onSaveInstanceState(outState);

        outState.putString("name", name);
    }

    public void showToast(String data){
        Toast.makeText(this, data, Toast.LENGTH_LONG).show();
    }
}
```

  * onCreate(), onStart(), onStop(), onDestroy() 메소드는 다음과 같은 시점에 구동되며, 그 시점마다 각각의 Toast 메세지를 출력하도록 구현하였다.
    * onCreate(): 액티비티가 화면에 출력되기 전에 메모리에 만들어지는 시점
    * onStart(): 액티비티가 화면에 출력되기 직전
    * onStop(): 액티비티가 화면에 출력되는 상태가 멈추는 시점
    * onDestroy(): 액티비티가 메모리에서 없어지는 시점
  * 가로-세로 방향을 전환할 때마다 서로 다른 액티비티가 재구동되는 것이므로 아무런 조치가 없다면 각 액티비티의 정보는 소실된다. 이를 방지하고 액티비티를 서로 연결하기 위해 사용하는 메소드가 onSaveInstanceState() 메소드이다.
  * editText에 임의의 텍스트를 입력하고 button을 누르게 되면 name 변수에 editText의 텍스트를 저장한다. 이후 액티비티가 소멸되었다가 다시 만들어질 때는 onSaveInstanceState() 메소드 안에서 name 변수의 값을 파라미터로 전달받은 Bundle 객체에 넣어준다. 이 Bundle 객체에 데이터를 넣으면 그 데이터는 단말에 저장되고, onCreate() 메소드가 호출될 때 파라미터로 전달된다.
  * 다만 editText의 텍스트는 위와 같은 조치가 없어도 액티비티 사이에서 소실되지 않는다.

<br>

## 화면 방향 전환에도 액티비티를 바꾸지 않고 레이아웃만 바꾸는 방법

```xml
<!--[AndroidManifest.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.orientation2">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.Orientation2">
        <activity android:name=".MainActivity"
            android:configChanges="orientation|screenSize|keyboardHidden">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```

```java
<!--[MainActivity.java]-->

package com.example.orientation2;

import androidx.appcompat.app.AppCompatActivity;

import android.content.res.Configuration;
import android.os.Bundle;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }

    public void onConfigurationChanged(Configuration newConfig){
        super.onConfigurationChanged(newConfig);

        if (newConfig.orientation == Configuration.ORIENTATION_LANDSCAPE) {
            showToast("방향: ORIENTATION_LANDSCAPE");
        } else if (newConfig.orientation == Configuration.ORIENTATION_PORTRAIT) {
            showToast("방향: ORIENTATION_PORTRAIT");
        }
    }

    public void showToast(String data){
        Toast.makeText(this, data, Toast.LENGTH_LONG).show();
    }
}
```

  * 화면 전환에도 불구하고 새로운 액티비티를 구동하지 않고 레이아웃만 변경하고 싶다면 위와 같이 코딩할 수 있다.
  * 단말의 방향이 바뀌는 것을 앱에서 이벤트로 전달받도록 하고 액티비티를 유지하려면 Manifest에 액티비티를 등록할 때 configChanges 속성을 설정하면 된다. 이후 MainActivity.java에서 onConfigurationChanged() 메소드를 재정의하면 추가적인 기능이 동작하도록 할 수 있다.
  * configChanges 속성 값이 결정되면 단말의 방향이 바뀌는 시점에 configurationChanged 메소드가 자동으로 호출된다.
  * 위 코드에서 configChanges 속성 중 keyboardHidden 값은 액티비티가 보일 때 키패드가 자동으로 나타나지 않도록 한다.
  * 액티비티의 방향을 세로 또는 가로로 고정시키고 싶다면 Manifest 파일에서 액티비티의 screenOrientation 속성 값을 landscape나 portrait으로 설정하면 된다.

**메소드 재정의 방법**: 메소드를 재정의하고 싶은 클래스를 클릭한 후 'Crtl + O' 를 누르거나 'Generate -> Override Methods'를 실행한다.
{: .notice--info}