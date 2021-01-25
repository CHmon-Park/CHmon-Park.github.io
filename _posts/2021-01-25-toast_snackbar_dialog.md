---
title: "Toast, Snackbar, and Dialog"
excerpt: "How to make and use Toast, Snackbar, and Dialog"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
  - toast
  - snackbar
  - dialog
  - LayoutInflater
  - 
last_modified_at: 2021-01-26T01:20:00
---
<!--more-->

<br>

## 토스트

  * 토스트는 간단한 메시지를 잠깐 보여주는 뷰로, 앱 위에 떠있는 뷰라고 할 수 있다.
  * 토스트는 포커스를 받지 않으므로 쉽고 간단하게 사용가능하며 디버깅 목적으로 사용하기에도 용이.

```xml
<!--[activity_main.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <EditText
            android:id="@+id/editText"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:textSize="20sp"
            android:hint="X 위치"
            android:inputType="numberSigned"
            />
        <!-- inputType="numberSigned" : 입력되는 데이터를 양수로 된 숫자만 가능하도록 제한 -->
        <EditText
            android:id="@+id/editText2"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:textSize="20sp"
            android:hint="Y 위치"
            android:inputType="numberSigned"
            />

        <Button
            android:id="@+id/button"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="띄우기"
            android:textSize="20sp"
            android:onClick="onButton1Clicked"/>
    </LinearLayout>

</LinearLayout>
```

```java
<!--[MainActivity.java]-->

package com.example.toast;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.Gravity;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.EditText;
import android.widget.TextView;
import android.widget.Toast;

import com.google.android.material.snackbar.Snackbar;

public class MainActivity extends AppCompatActivity {
    EditText editText;
    EditText editText2;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = findViewById(R.id.editText);
        editText2 = findViewById(R.id.editText2);

    }

    public void onButton1Clicked(View v) {
        try {
            Toast toastView = Toast.makeText(this, "위치가 바뀐 토스트 메시지입니다.", Toast.LENGTH_SHORT);

            int xOffset = Integer.parseInt(editText.getText().toString());
            int yOffset = Integer.parseInt(editText2.getText().toString());

            toastView.setGravity(Gravity.TOP|Gravity.TOP, xOffset, yOffset);
            toastView.show();

        } catch (NumberFormatException e) {
            e.printStackTrace();
        }
    }

}
```

  * makeText 메소드의 첫 번째 인자인 Context 객체는 일반적으로 Context 클래스를 상속한 액티비티를 사용할 수 있으며, 액티비티를 참조할 수 없는 경우에는 getApplicationContext() 메소드를 호출하면 Context 객체가 반환된다.
  * 위의 코드는 토스트의 위치를 변경하여 출력하도록 하는 코드이다.
  * 위치 변경을 위해 setGravity() 메소드를 사용하여 값을 설정하지만, Android R(11) 부터 text Toast는 설정 기능이 no-op가 되어 gravity나 margin을 customize 할 수 없게 되었다.
  * 공식 문서에서도 Toast의 gravity나 margin 등을 임의로 지정하는 것을 말리는 추세이다.
  * 대안으로는 text Toast를 simple Toast로 사용하여 gravity와 margin을 지정하는 방법이 있다.(아래 코드)

**text Toast vs simple Toast**: text Toast는 Toast.makeText 메소드를 이용하여 만드는 
{: .notice--info}
  
```xml
<!--[activity_main.xml]-->
<!--중략-->

    <Button
        android:id="@+id/button2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="모양 바꿔 띄우기"
        android:onClick="onButton2Clicked"/>

<!--중략-->
```

```java
<!--[MainActivity.java]-->
<!--중략-->

    public void onButton2Clicked(View view) {
        LayoutInflater inflater = getLayoutInflater();

        View layout = inflater.inflate(R.layout.toastborder, (ViewGroup) findViewById(R.id.toast_layout_root));         // XML로 정의된 레이아웃을 메모리에 객체화

        TextView text = layout.findViewById(R.id.text);

        Toast toast = new Toast(this);
        text.setText("모양 바꾼 토스트");
        toast.setGravity(Gravity.CENTER, 0, -100);
        toast.setDuration(Toast.LENGTH_SHORT);
        toast.setView(layout);
        toast.show();
    }
    
<!--중략-->
```

```xml
<!--[toastborder.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/toast_layout_root"
    android:orientation="horizontal"
    android:padding="10dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/text"
        android:padding="20dp"
        android:textSize="32sp"
        android:background="@drawable/toast"/>

</LinearLayout>
```

```xml
<!--[toast.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <stroke
        android:width="4dp"
        android:color="#ff487080"/>
    <solid
        android:color="#ff354000"/>
    <padding
        android:left="20dp"
        android:top="20dp"
        android:right="20dp"
        android:bottom="20dp"/>
    <corners
        android:radius="15dp"/>
    
</shape>
```

  * 위의 코드는 초기 코드에서 추가된 내용으로, 토스트의 위치와 모양까지 바꾼 simple Toast이다.
  * LayoutInflater를 이용하여 xml로 정의된 layout을 메모리에 객체화 하고, Toast 클래스를 이용해 gravity를 지정하였다. Toast 클래스르로 따로 인스턴스를 만드는 것이 바로 simple Toast 방식이다.
  * 코드의 순서는 다음과 같다. <br> [MainActivity.java 에서 toastborder.xml 을 객체화] -> [Toast가 생성될 toastborder.xml 의 TextView에서 background로 toast.xml을 지정] -> [toast.xml이 토스트의 모양과 색상 지정]

<br>

## 스낵바

  * 스낵바는 외부 라이브러리로 추가되었기 때문에 스낵바가 들어 있는 Material Library를 프로젝트에 추가해야 함. 현재의 안드로이드 스튜디오 버전은 이를 미리 구비한 것으로 보임.

```xml
<!--[activity_main.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button3"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="스낵바 띄우기"
        android:onClick="onButton3Clicked"/>

</LinearLayout>
```

```java
<!--[MainActivity.java]-->
<!--중략-->

    public void onButton3Clicked(View view) {
        Snackbar.make(view, "스낵바입니다.", Snackbar.LENGTH_LONG).show();
    }

<!--중략-->
```

  * 스낵바는 화면 아래쪽에서 올라오기 때문에 아래쪽의 화면 일부분을 가리지만, 토스트와는 다른 방식이기에 사용자에게 선택지를 준다.

<br>

## 알림 대화상자

  * 알림 대화상자는 사용자에게 확인을 받거나 선택하게 할 때 사용한다.

```xml
<!--[activity_main.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="버튼을 누르면 대화상자가 뜹니다."
        android:textSize="25sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.248" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="띄우기"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView"
        app:layout_constraintVertical_bias="0.223" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

```java
<!--[MainActivity.java]-->

package com.example.dialog;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.app.Dialog;
import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    TextView textView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = findViewById(R.id.textView);

        Button button = findViewById(R.id.button);
        button.setOnClickListener(new View.OnClickListener(){

            @Override
            public void onClick(View v) {
                showMessage();
            }
        });
    }

    private void showMessage() {
        AlertDialog.Builder builder = new AlertDialog.Builder(this);
        builder.setTitle("안내");
        builder.setMessage("종료하시겠습니까?");
        builder.setIcon(android.R.drawable.ic_dialog_alert);

        builder.setPositiveButton("예", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                String message = "예 버튼이 눌렸습니다.";
                textView.setText(message);
            }
        });

        builder.setNeutralButton("취소", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                String message = "취소 버튼이 눌렸습니다.";
                textView.setText(message);
            }
        });

        builder.setNegativeButton("아니오", new DialogInterface.OnClickListener() {
            @Override
            public void onClick(DialogInterface dialog, int which) {
                String message = "아니오 버튼이 눌렸습니다.";
                textView.setText(message);
            }
        });

        AlertDialog dialog = builder.create();
        dialog.show();
    }
}
```

  * AlertDialog 클래스는 알림 대화상자를 보여주는 가장 단순한 방법을 제공한다.
  * Dialog 클래스가 대화상자의 기본 클래스이지만, Dialog를 직접 인스턴스화 하려는 시도는 지양하는 것이 좋다. 대신하여 AlertDialog나 DatePickerDialog, TimePickerDialog 를 사용하는 것이 추천된다.
  * setTitle() 메소드로 제목, setMessage() 메소드로 알림 내용, setIcon() 메소드로 안내 아이콘을 지정한다.
  * PositiveButton, NegativeButton, NeutralButton 은 각각 하나씩만 존재 가능하며, 각 위치는 미리 지정되어 있다.
  * 버튼의 모양, 위치, 색상을 커스터마이징하는 방법은 아래와 같다.<br>

```java
    AlertDialog.Builder builder = new AlertDialog.Builder(this);
    AlertDialog alert = builder.create();           // Dialog를 만들어 객체를 가져옴.
    alert.show();                                   // AlertDialog의 버튼은 Dialog가 동적으로 생성될 때 생성되기에 Dialog를 먼저 출력하는 것이 필요하다. 
    Button btn = alert.getButton(AlertDialog.BUTTON_POSITIVE);      // 이후 Dialog에서 버튼을 임의로 가져온다.
    
    <!--이후 btn.setTextColor, btn setBackground 등등...--> 
```