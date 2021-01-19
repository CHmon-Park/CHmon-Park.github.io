---
title: "Layout Code in Java"
excerpt: "How to make a Layout in Java Code"
excerpt_separator: "<!--more-->"
categories:
  - Android Application
tags:
  - Android
  - Application
  - Android Studio
  - Java
  - Layout
  - XML
last_modified_at: 2021-01-14T18:30:00
---
<!--more-->

<br>

## 자바 코드에서 화면 구성하기

```java
[LayoutCodeActivity.java]

중략...

public class LayoutCodeActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        LinearLayout mainLayout = new LinearLayout(this);
        mainLayout.setOrientation(LinearLayout.VERTICAL);

        LinearLayout.LayoutParams params =
                new LinearLayout.LayoutParams(
                        LinearLayout.LayoutParams.MATCH_PARENT,
                        LinearLayout.LayoutParams.WRAP_CONTENT
                );

        Button button1 = new Button(this);
        button1.setText("Button1");
        button1.setLayoutParams(params);
        mainLayout.addView(button1);

        setContentView(mainLayout);
    }
}
```

```xml
<activity android:name=".LayoutCodeActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        
        <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>
</activity>
```

  * 화면 레이아웃을 미리 만들 수 없는 경우 또는 필요할 때마다 바로바로 레이아웃을 만들어야 하는 경우에는 자바 소스 코드에서 화면 레이아웃을 구성해야 할 수도 있다.
  * 사용자가 입력한 데이터나 파일에서 읽어 들인 데이터 또는 네트워킹을 통해 서버에서 받아온 데이터의 유형에 따라 화면의 구성을 바꾸고 싶을 때에는 XML로 정의하는 것보다 자바 코드에서 화면을 구성하는 것이 효율적이다.
  * LayoutParams 객체는 뷰 배치를 위한 속성을 설정할 때 사용된다. 속성을 담은 LayoutParams 객체를 setLayoutParams로 뷰에 적용할 수 있다.
  * 레이아웃에 뷰를 추가하려면 addView() 메서드를 사용한다.

**Context 객체**: 위의 코드 중 'this'라는 키워드는 Context 객체가 전달된 것으로, new 연산자를 이용해 뷰 객체를 코드에서 만들 때는 항상 Context 객체가 전달되어야 한다. 이 Context 객체는 프로그래밍 언어 상에서는 객체의 정보를 담고 있는 객체를 의미한다. 
위 코드의 경우 AppCompatActivity 클래스가 Context를 상속하고 있으므로 'this'라는 표현으로 Context 객체를 사용할 수 있지만, Context를 상속받지 않은 클래스에서 Context 객체를 전달해야 한다면 getApplicationContext라는 메서드를 호출하여 앱에서 참조 가능한 Context 객체를 사용할 수 있다.
{: .notice--info}