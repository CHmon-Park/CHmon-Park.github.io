---
title: "Start of Django"
excerpt: "Introduction of Django and the way to use it"
excerpt_separator: "<!--more-->"
categories:
  - Django
tags:
  - Django
last_modified_at: 2021-07-19T16:11:00
---

<!--more-->

<br>

## Django

- 장고(Django)는 파이썬 기반 웹 프레임워크로, 쉬운 설치 및 작업과 다양한 기능들이 있다는 점이 장점이다.
- 아래는 장고의 특징들이다.
  1. MVC(Model-View-Controller) 패턴 기반 MVT(Model-View-Template)
  2. 객체 관계 매핑: 데이터베이스와 모델을 연결시키는 ORM(Object-Relational Mapping) 기능을 통해 SQL 문장 없이도 테이블을 조작할 수 있다.
  3. 자동으로 구성되는 관리자 화면
  4. 직관적이면서도 유연한 URL 설계(정규표현식도 가능)
  5. 자체 템플릿 시스템
  6. 캐시 시스템 사용으로 재사용 성능 향상
  7. 다국어 지원
  8. 테스트용 웹서버 포함
  9. 소스 변경사항 자동 반영

## Django 설치

- 파이썬 최신 버전 설치
- (윈도우에서) pip(Python Install Package) 프로그램을 통해 장고 설치
  - pip install Django
- 장고 프로그램 최신 버전으로 업데이트
  - pip install Django --upgrade

## Django 시작하기

- Django 프로젝트 생성
  - django-admin startproject &lt;mysite&gt;
- Django Application 생성
  - python manage.py startapp polls
  - 본 명령어는 프로젝트의 루트 디렉토리(manage.py가 있는 곳)에서 사용해야 함.
- settings.py 파일 조정
  - ALLOWED_HOSTS 항목 조정: DEBUG=True 이면 개발 모드, False 이면 운영 모드로 인식하게 되는데, 개발 모드의 경우 값을 따로 지정하지 않더라도 'localhost'와 '127.0.0.1'로 간주하나, 운영 모드의 경우에는 반드시 서버의 IP나 도메인을 지정해야 한다.
  - 애플리케이션 등록: 프로젝트에 포함되는 애플리케이션은 INSTALLED_APPS에 등록이 되어야 한다.
  - 사용하고자 하는 데이터베이스 엔진 등록(default는 sqlite3)
  - TIME_ZONE / LANGUAGE 지정
- 기본 테이블 생성
  - python manage.py migrate
  - 본 명령어는 프로젝트의 생성 초기나 데이터베이스에 변경사항이 있을 경우 이를 반영해주는 명령어이다.
- 웹 서버 작동해보기
  - python manage.py runserver
- Django가 가지고 있는 관리자 화면에 접속하기
  - 서버 IP 주소 뒤에 '/admin'을 추가하게 되면 관리자 페이지로 이동한다.
  - 관리자 페이지에는 로그인이 필요하므로 아래의 명령어를 통해 관리자용 계정을 미리 만들어야 한다.
    - python manage.py createsuperuser
