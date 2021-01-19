---
title: "Basic Widgets"
excerpt: "What is Widget / Examples of Widget"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
  - widget
  - textview
  - button
  - imageview
  - edittext
last_modified_at: 2021-01-16T17:00:00
---
<!--more-->

<br>

## 텍스트뷰(TextView)

#### 텍스트뷰의 속성

  * text: 필수
  * textColor: ex)AARRGGBB
  * textSize: sp, dp, px 등의 단위중 sp를 권장
  * testStyle: 문자열의 스타일 속성(normal, bold, italic 등). '|'를 이용하여 복수의 속성을 동시 지정도 가능.
  * typeFace: 폰트 지정(기본-normal, sans, serif, monospace). 기본 폰트 이외의 폰트를 지정할 때는 앱에 등록 후 설정 가능.
  * maxLines: 텍스트뷰에서 표시하는 문자열의 최대 줄 수 설정.

#### 텍스트뷰의 text를 strings.xml 파일에서 설정하는 방법

```xml
<!--[app/res/values/strings.xml]-->

<resources>
    <string name="app_name">SampleWidget</string>
    <string name="person_name">CHPark</string>
</resources>
```

```xml
<!--[activity_main.xml]-->
<!--strings.xml을 이용하여 text 지정-->

    <TextView
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="@string/person_name" 
        android:textColor="#AA294395"
        android:textSize="40sp"
        android:textStyle="bold|italic"
        android:typeface="serif"
        android:maxLines="1"/>
```

**strings.xml을 이용하여 다국어 지원**: /app/res/ 경로 아래에 values-kr, values-en과 같이 로케일 이름을 붙인 폴더를 생성하고 그 안에 각 언어에 맞는 text를 기입한 strings.xml 파일을 생성하면, 앱의 언어 설정이 바뀔 때 자동으로 해당하는 로컬의 언어 strings.xml을 로딩한다.
{: .notice--info}

<br>

## 에디트텍스트(EditText)

```xml
<!--[edittext.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">

    <EditText
        android:id="@+id/usernameInput"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="24sp"
        android:inputType="text"
        android:hint="이름을 입력하세요." />
</LinearLayout>
```

  * hint 속성은 에디트 텍스트 내에 어떤 내용을 입력하면 되는지 표시해주는 안내 문구를 지정할 수 있다.
  * inputType 속성은 입력되는 글자의 유형을 정의할 수 있다.

<br>

#### 텍스트뷰와 에디트텍스트의 다른 속성들

  * 커서 관련 메소드 및 속성
    * public int getSelectionStart(): 선택된 영역의 시작 위치 리턴(선택 영역 없을 경우 커서 위치 리턴)
    * public int getSelectionEnd(): 선택된 영역의 끝 위치 리턴(선택 영역 없을 경우 커서 위치 리턴)
    * public void setSelection(int start, int stop): 선택 영역 지정
    * public void setSelection(int index): 커서 위치 지정
    * public void selectAll(): 전체 선택
    * public void extendSelection(int index): 선택 영역 확장
    * selectAllOnFocus: true로 설정 시 포커스를 받을 때 문자열 전체 선택
  * 자동 링크 관련 속성
    * autoLink: true로 설정 시 문서에 포함된 웹페이지 주소나 이메일 주소를 링크 색상으로 표시하고 링크를 누르면 해당 웹페이지 접속
  * 줄 간격 조정 관련 속성
    * lineSpacingMultiplier: 현재 줄 간격을 기본 줄 간격의 배수로 지정할 때 사용
    * lineSpacingExtra: 현재 줄 간격에 여유값을 두기 위해 사용
  * 대소문자 표시 관련 속성
    * capitalize: 속성 값으로 'characters', 'words', 'sentences' 등을 지정하면 글자, 단어, 문장 단위로 대소문자를 조절할 수 있음
  * 줄임 표시 관련 속성
    * ellipsize: 속성 값 중 'none'은 뒷부분을 자르고, 'start', 'middle', 'end'는 각각 앞부분, 중간, 끝 부분을 잘라서 보여준다.
  * 힌트 표시 관련 속성
    * hintColorHint: 힌트 문구의 색을 지정
  * 편집 가능 관련 속성
    * editable: 속성 값을 true로 하면 편집 가능, false로 하면 편집 불가
  * 문자열 변경 처리 관련 속성
    * public void addTextChangedListener(TextWatcher watcher)
    * getText.toString()

<br>

## 버튼(Button)

  * 버튼은 텍스트뷰를 상속하여 정의되어 있기에 텍스트뷰의 속성도 그대로 가지고 있다.
  * 텍스트뷰의 속성보다 확장성을 가진 체크박스와 라디오 버튼을 알아보자.

```xml
<!--[button.xml]-->

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/button"
        android:text="선택"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"/>

    <RadioGroup
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/radioGroup01"
        android:orientation="horizontal"
        android:layout_marginTop="20dp"
        android:paddingLeft="10dp"
        android:paddingRight="10dp">

        <RadioButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/radio01"
            android:text="남성"
            android:textColor="#ff55aaff"
            android:textStyle="bold"
            android:textSize="24sp"/>
        <RadioButton
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/radio02"
            android:text="여성"
            android:textStyle="bold"
            android:textSize="24sp"/>
    </RadioGroup>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center_vertical|center_horizontal"
        android:orientation="horizontal"
        android:paddingTop="20dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="하루종일"
            android:textSize="24sp"
            android:paddingRight="10dp"
            android:textColor="#ff55aaff"
            />
        <CheckBox
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/allDay"/>
    </LinearLayout>

</LinearLayout>
```

  * 체크 박스와 라디오 버튼은 단순히 클릭 이벤트만 처리하는 것이 아니라 상태 값을 저장하고 선택/해제 상태를 표시할 수 있도록 CompoundButton 클래스에 다음과 같은 메소드가 정의되어 있다.
    * public boolean isChecked()        // 체크 상태 확인
    * public void setCheck (boolean checked)        // 체크 지정
    * public void toggle()
    * void onCheckChanged(CompoundButton buttonView, boolean isChecked)     // 버튼의 상태가 바뀌는 것을 알고 싶을 때 재정의하여 사용
  * 라디오 버튼의 경우 하나의 버튼 선택 시 다른 버튼을 선택했던 상태가 해제된다. 이를 위해 라디오 버튼들은 라디오 그룹에 묶어야 한다.
  * 버튼에 아이콘을 넣기 위해서는 ImageButton 태그를 사용할 수 있다.

<br>

