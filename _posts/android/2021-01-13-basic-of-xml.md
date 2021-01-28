---
title: "Basic of XML Files"
excerpt: "What is XML / Features of XML"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
  - XML
last_modified_at: 2021-01-13T19:21:00
---
<!--more-->
<br>

## XML의 기본 속성

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">
```


1. ```xml
   <?xml version="1.0" encoding="utf-8"?>
   ```
  * 현 파일이 xml 형식이며 인코딩이 'utf-8'으로 되어 있음을 의미.
2. ```xml
   androidx.constraintlayout.widget.ConstraintLayout
   ```
  * Component Tree 창의 계층도에서 가장 위쪽에 있으므로 최상위 레이아웃.
  * ConstraintLayout 이전에 들어간 부분은 패키지를 의미하며, 안드로이드 기본 API에 포함되어 있다면 표기가 생략될 수 있으나, 외부 라이브러리에서 불러온 것이라면 패키지 이름이 같이 기입되어야 한다.
3. ```xml
   xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto"
   xmlns:tools="http://schemas.android.com/tools"
   ```
  * xmlns:android 속성은 하나의 파일에 한 번만 사용하면 되며, xmlns 뒤에 있는 android 라는 이름이 다른 속성의 접두어(prefix)로 사용된다.
  * 예를 들어, android:layout_width 속성에서 android: 는 xmlns:android 로 지정된 정보를 참조하여 사용한다.
  * xmlns 접두어 종류와 의미
    * xmlns:android - 안드로이드 기본 SDK에 포함되어 있는 속성을 사용
    * xmlns:app - 외부 라이브러리에 포함되어 있는 속성을 사용. app이라는 단어는 다른 단어로 바꿀 수 있음.
    * xmlns:tools - 안드로이드 스튜디오의 디자이너 도구 등에서 화면에 보여줄 때 사용. 앱이 실행될 때는 적용되지 않고 안드로이드 스튜디오에서만 적용.
    
## 기타 속성
1. ```xml
       <Button
            android:id="@+id/button3"
   ```
  * id 속성은 뷰를 구분하는 구분자 역할을 함.
  * 코드 상에서는 '@+id/아이디값'의 형태로 기입됨.
2. 크기 표시 단위
  * px - 화면 픽셀의 수
  * dp - 160dpi 화면을 기준으로 한 픽셀
  * sp - 텍스트 크기를 지정할 때 사용하는 단위(글꼴 마다 1sp당 픽셀수가 달라짐)
  * in - 1인치로 된 물리적 길이
  * mm - 1밀리미터로 된 물리적 길이
  * em - 글꼴과 상관없이 동일한 텍스트 크기 표시