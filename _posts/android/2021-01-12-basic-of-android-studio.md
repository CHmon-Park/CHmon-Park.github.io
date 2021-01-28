---
title: "Basic of Android Studio"
excerpt: "Definition and feature of Android / What is Android Studio"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
last_modified_at: 2020-01-12T17:38:00
---
<!--more-->
<br>
# **안드로이드**

### 안드로이드란 무엇인가?
  * 구글(Google)에서 만든 스마트폰용 운영체제(Operating System)
  * 휴대용 단말기에서 이용되며, 다양한 앱을 실행할 수 있도록 구성된 앱 플랫폼(Platform)

### 안드로이드의 장점
  * 오픈 소스
  * 자바 개발 언어
  * 스마트폰을 위한 완벽한 컴포넌트 제공
  * 쉬운 앱 간 연동
  * 다양한 기능 지원

<br>

# **안드로이드 스튜디오 알아보기**
안드로이드 스튜디오란 안드로이드 운영체제에서 사용할 수 있는 앱을 간편하게 만들 수 있도록 하는 IDE(Integrated Development Environment)이다.

### Main Activity.java
```java
package org.ddd.fff;

import ...

public class MainActivity extends AppCompatActivity {
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
  * MainActivity.java는 OnCreate() 함수를 통해 어플리케이션의 시작점 역할을 한다.
  * super 키워드는 MainActivity.java가 상속을 받은 클래스인 AppCompatActivity 클래스로부터 데이터를 받아오는 것으로, 부모 클래스의 OnCreate() 함수를 호출한다.
  * setContentView() 함수는 그 안의 파라미터를 화면에 띄워주는 역할을 한다. 

### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
  * MainActivity.java에서 볼 수 있었던 R.layout.activity_main 이란 코드는 /res/layout 폴더 안에 들어 있는 activity_main.xml을 의미한다.
  * 기본적으로 프로젝트를 생성했을 때 이 activity_main.xml이 가장 먼저 화면에 출력되도록 설정되어 있다. 이 사항은 /manifests/ 폴더의 AndroidManifest.xml 에서 수정할 수 있다.
  * 즉, xml 파일들은 어플리케이션의 각 화면을 의미한다고 할 수 있다.
  * 화면을 수정함에 있어서 소스 코드를 직접 수정하는 방법과 디자인 탭에서 간편하게 진행하는 방법이 있다.

<br>

### **기본적 예시**
**Auto Import**: [File > Settings > Editor > General > Auto Import]
{: .notice--info}
#### OnButtonClicked

```xml
[activity_main.xml]

중략..

    <Button android:id = "@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:onClick="onButton1Clicked"
        android:text="확인1"
        
        중략..
        
        />
```
```java
[MainActivity.java]

중략...

public class MainActivity extends AppCompatActivity {
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    
    public void onButton1Clicked(View v) {
        Toast.makeText(this, "확인1 버튼이 눌렸어요!", Toast.LENGTH_LONG).show.();
    }
}
```
  * xml 파일의 버튼을 이용해 이벤트를 처리하기 위해서는 논리적 작업이 이루어지는 자바 소스와 연결하는 과정이 필요하다.
  * 이를 위해 xml 파일의 Button 속성 중 onClick 속성에 Java 파일의 이벤트 함수를 지정한다.
  * Toast 클래스는 makeText() 메서드와 show() 메서드를 사용하여 화면에 메세지를 잠깐 출력했다 없앨 수 있다.

<br>

#### 인터넷 접속하기, 전화 걸기

```java
중략...

    public void onButton2Clicked(View v) {
        Intent myIntent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://m.naver.com")); // Intent란 안드로이드 플랫폼에 원하는 것을 말할 때 쓰이는 도구
        startActivity(myIntent);
    }

    public void onButton3Clicked(View v) {
        Intent myIntent = new Intent(Intent.ACTION_VIEW, Uri.parse("tel:010-1000-1000"));
        startActivity(myIntent);
    }
```
  * Intent란 안드로이드 플랫폼에게 원하는 것을 말할 때 전달하는 우편물 같은 것.
  * URI란 통합 자원 식별자(Uniform Resourse Identifier, URI)로서, 인터넷에 있는 자원을 나타내는 유일한 주소이다. 흔히 알고 있는 URL(Uniform Resource Name, 통합 자원 이름)은 자원의 위치만을 알려주기에 URI가 더 넓은 의미를 가진다고 할 수 있다.<br>Example: **http://opentutorials.org:3000/main?id=HTML&page=12** <br> [블로그 참고](https://velog.io/@jch9537/URI-URL)
  * Parsing 이란 구문 분석 과정을 의미한다. 문장이 담고 있는 데이터를 분해 및 분석하여 원하는 형태로 재조립 및 가공하는 과정이다. 다른 형식으로 저장된 데이터를 원하는 형식의 데이터로 변환하는 것이라고 볼 수도 있다.  