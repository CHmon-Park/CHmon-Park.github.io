---
title: "ScrollView and Bitmap Image Change(Code)"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
  - Code
  - ScrollView
  - Bitmap
last_modified_at: 2021-01-14T22:50:00
---
<!--more-->

<br>

## 두 개의 이미지뷰에 이미지 번갈아 보여주기

```xml
[activity_main.xml]

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity"
    android:orientation="vertical">

    <HorizontalScrollView
        android:id="@+id/horscrollView1"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1">

        <ScrollView
            android:id="@+id/scrollView1"
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <FrameLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent">
                <ImageView
                    android:id="@+id/imageView1"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:visibility="visible"/>
                <ImageView
                    android:id="@+id/imageView2"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:visibility="invisible"/>
            </FrameLayout>


        </ScrollView>
    </HorizontalScrollView>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:gravity="center">

        <Button
            android:id="@+id/button1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="상"
            android:layout_margin="10dp"
            android:onClick="onButton1Clicked"/>
        <Button
            android:id="@+id/button2"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="하"
            android:layout_margin="10dp"
            android:onClick="onButton2Clicked"/>

    </LinearLayout>

    <HorizontalScrollView
        android:id="@+id/horscrollView2"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1">

        <ScrollView
            android:id="@+id/scrollView2"
            android:layout_width="match_parent"
            android:layout_height="match_parent">
            <FrameLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent">
                <ImageView
                    android:id="@+id/imageView3"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:visibility="invisible"/>
                <ImageView
                    android:id="@+id/imageView4"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:visibility="visible"/>
            </FrameLayout>

        </ScrollView>
    </HorizontalScrollView>
</LinearLayout>
```

```java
[MainActivity.java]

package com.example.mission03;

import androidx.appcompat.app.AppCompatActivity;

import android.content.res.Resources;
import android.graphics.drawable.BitmapDrawable;
import android.os.Bundle;
import android.view.View;
import android.widget.ImageView;
import android.widget.ScrollView;

public class MainActivity extends AppCompatActivity {
    ScrollView scrollview1;
    ScrollView scrollview2;
    ImageView imageView1;
    ImageView imageView2;
    ImageView imageView3;
    ImageView imageView4;
    BitmapDrawable bitmap1;
    BitmapDrawable bitmap2;


    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        scrollview1 = findViewById(R.id.scrollView1);
        scrollview2 = findViewById(R.id.scrollView2);
        imageView1 = findViewById(R.id.imageView1);
        imageView2 = findViewById(R.id.imageView2);
        imageView3 = findViewById(R.id.imageView3);
        imageView4 = findViewById(R.id.imageView4);

        scrollview1.setHorizontalScrollBarEnabled(true); // 수평 스크롤바 사용 기능 설정
        scrollview2.setHorizontalScrollBarEnabled(true);

        Resources res1 = getResources();            // 리소스 이미지 참조
        bitmap1 = (BitmapDrawable) res1.getDrawable(R.drawable.megacharizard_x);
        int bitmapWidth1 = bitmap1.getIntrinsicWidth();
        int bitmapHeight1 = bitmap1.getIntrinsicHeight();

        imageView1.setImageDrawable(bitmap1);           // 이미지 리소스와 이미지 크기 설정
        imageView1.getLayoutParams().width = bitmapWidth1;
        imageView1.getLayoutParams().height = bitmapHeight1;

        Resources res2 = getResources();
        bitmap2 = (BitmapDrawable) res2.getDrawable(R.drawable.megacharizard_x);
        int bitmapWidth2 = bitmap2.getIntrinsicWidth();
        int bitmapHeight2 = bitmap2.getIntrinsicHeight();

        imageView3.setImageDrawable(bitmap2);
        imageView3.getLayoutParams().width = bitmapWidth2;
        imageView3.getLayoutParams().height = bitmapHeight2;
    }

    public void onButton1Clicked (View v) {
        changeImage(0);
    }

    public void onButton2Clicked (View v) {
        changeImage(1);
    }

    private void changeImage(int n) {
        if (n == 0) {
            imageView1.setVisibility(View.VISIBLE);
            imageView2.setVisibility(View.INVISIBLE);
            imageView3.setVisibility(View.INVISIBLE);
            imageView4.setVisibility(View.VISIBLE);
        } else if (n == 1) {
            imageView1.setVisibility(View.INVISIBLE);
            imageView2.setVisibility(View.VISIBLE);
            imageView3.setVisibility(View.VISIBLE);
            imageView4.setVisibility(View.INVISIBLE);
        }
    }
}
```

  * 리니어레이아웃 내에 두 개의 프레임 레이아웃을 두고, 그 안에 각각 두 개의 이미지뷰를 두어 눌리는 버튼에 따라 이미지뷰들의 visible을 조작하여 전환 효과를 출력한다.
  * java 파일에서 이미지 파일을 이미지뷰에 설정하였는데, 이 때 사용한 메소드는 setImageDrawable()이다. 이 메소드는 인자로 Drawable 객체의 이미지 파일을 인자로 받으므로, 이미지들은 getDrawable() 메소드를 이용해 BitmapDrawable 객체로 만들어졌다.
  * setImageDrawable() 메소드는 이미지뷰가 이미지의 크기를 화면 크기에 맞게 자동으로 조절하기에, getIntrinsicWidth(), getIntrinsicHeight() 메소드를 통해 이미지의 원래 크기를 알아내어 getLayoutParams() 메소드를 통해 직접 설정하였다.

#### 보완해야 할 사항

  * 위와 아래의 이미지뷰에 있는 두 이미지가 버튼 조작에 따라 각각 새로이 이미지를 설정하는 것이 가장 바람직한 방향이라 생각했으나, 코드 상의 메소드들에 대한 이해가 부족했다는 점과 코딩의 편의상 이미지뷰들의 visibility를 이용해 간단히 구현하였다. 그러나 이는 진정으로 이미지를 바꾸는 효과라고 보기는 힘들다. 
    말그대로 visibility가 재조정되는 형식이기 때문에, 만약 스크롤뷰를 통해 이미지의 일정 영역으로 화면이 옮겨졌을 경우 버튼 조작에 따라 이미지가 바뀌었다가 다시 돌아와도 같은 영역을 화면에 출력하게 된다. 즉, 이미지가 새로 설정되는 느낌을 줄 수가 없다는 한계가 있다.   