.. toctree::
  :maxdepth: 2
    

Django 2 ตอนที่ 2
=================

การสร้างเว็บด้วย Django 2 ตอนที่ 2

> การใช้ bootstrap ใน view

เลือก bootstrap
-------------------

1. เลือก theme สามารถเลือก theme และ download ได้จาก เว็บไซต์ของ bootstrap ทั่วไป เช่น

  + https://getbootstrap.com

  + https://bootswatch.com

  + สมมติว่าใช้ https://bootswatch.com/solar

2. เตรียมไฟล์ต่อไปนี้

  + index.html

  + bootstrap.min.css

3. จัดเตรียม folders ต่อไปนี้

.. code-block:: sh

  mkdir -p myapp/templates/myapp/
  mkdir -p myapp/static/myapp/css/
  mkdir -p myapp/static/myapp/js/

4. จัดเก็บไฟล์ในข้อ 2. 

  + เก็บ `myapp.html` ไว้ที่ `myapp/templates/myapp/` 

  + เก็บ `bootstrap.min.css` ไว้ที่ `myapp/static/myapp/css/`

เริ่มพัฒนาเว็บ
------------------

1. แก้ไข `myapp/views.py` เป็น

.. code-block:: python

  from django.shortcuts import render

  def index(req):
    return render(req, 'myapp/index.html')


2. สร้างไฟล์ `myapp/templates/myapp/base.html` โดยมีคำสั่งต่อไปนี้

.. code-block:: html

  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <meta http-equiv="X-UA-Compatible" content="ie=edge">
      <title> Calendar App</title>
      {% load static %}
      <link rel="stylesheet" href="{% static 'myapp/css/bootstrap.min.css' %}" />
    </head>
    <body>
      <div class="navbar navbar-expand-lg fixed-top navbar-dark bg-dark">
        <div class="container">
          <a href="/" class="navbar-brand">Calendar</a>
          <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarResponsive" aria-controls="navbarResponsive" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarResponsive">
            <ul class="navbar-nav">
              <li class="nav-item">
                <a class="nav-link" href="../help/">Help</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="http://blog.bootswatch.com">Blog</a>
              </li>
              <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" data-toggle="dropdown" href="#" id="download">Solar <span class="caret"></span></a>
                <div class="dropdown-menu" aria-labelledby="download">
                  <a class="dropdown-item" href="https://jsfiddle.net/bootswatch/mqoc3ah6/">Open in JSFiddle</a>
                  <div class="dropdown-divider"></div>
                  <a class="dropdown-item" href="../4/solar/bootstrap.min.css">bootstrap.min.css</a>
                  <a class="dropdown-item" href="../4/solar/bootstrap.css">bootstrap.css</a>
                </div>
              </li>
            </ul>

            <ul class="nav navbar-nav ml-auto">
              <li class="nav-item">
                <a class="nav-link" href="http://builtwithbootstrap.com/" target="_blank">Built With Bootstrap</a>
              </li>
              <li class="nav-item">
                <a class="nav-link" href="https://wrapbootstrap.com/?ref=bsw" target="_blank">WrapBootstrap</a>
              </li>
            </ul>

          </div>
        </div>
      </div>
      {% block content %}

      {% endblock %}
    </body>
  </html>

3. สร้างไฟล์ `myapp/templates/myapp/index.html`

.. code-block:: html

  {% extends 'myapp/base.html' %}
  {% block content %}
  <div class="container">
  </div>
  {% endblock %}

ภาพเว็บไซต์เมื่อหน้าจอขนาดเล็ก

.. image:: images/addboots-small.png

ภาพเว็บไซต์เมื่อหน้าจอขนาดกลาง

.. image:: images/addboots-medium.png

4. สร้าง div แสดงข้อมูลสำหรับ calendar

สร้างไฟล์ชื่อ `myapp/templates/myapp/_calendar_entry.html` โดยมีคำสั่งต่อไปนี้

.. code-block:: html

  <div class="calendar_entry col-lg-4">
    <br/>
    <h2>กิจกรรมสาขา</h2>
    <h4>24 ต.ค. 2561</h4>
    <p>
      ถึงน้องๆทุกคน พี่ปี 4 อยากให้เข้าร่วมกิจกรรม น้องติวพี่่ พี่เรียนกับน้อง
    </p>
    <button class="btn btn-primary">ดูรายละเอียด</button>
  </div>

5. ปรับ `index.html` เป็น

.. code-block:: html

  {% extends 'myapp/base.html' %}
  {% block content %}
  <div class="container">
    <div class="row">
      {% include 'myapp/_calendar_entry.html' %}
    </div>
  </div>
  {% endblock %}

ผลลัพธ์

.. image:: images/addentry-small.png

6. เขียนนิยามของ กิจกรรม เพื่อสร้าง table ในฐานข้อมูล

แก้ไขไฟล์ชื่อ `myapp/models.py` ตามนี้

.. code-block:: python

  from django.db import models

  class Entry(models.Model):
      name = models.CharField(max_length=100)
      date = models.DateTimeField()
      description = models.TextField()
      created = models.DateTimeField(auto_now_add=True)

      def __str__(self):
        return f'{self.name} {self.date}'

7. สร้างฐานข้อมูล

> ปิด server ก่อน  Ctrl+C

.. code-block:: sh

  ./manage.py makemigrations
  ./manage.py migrate
  ./manage.py runserver

8. ทำ admin สามารถสร้าง entry ได้

แก้ไขไฟล์ `myapp/admin.py` เป็นดังนี้

.. code-block:: python

  from django.contrib import admin
  from .models import Entry

  admin.site.register(Entry)

เมื่อเข้าใช้เป็น admin ที่ `http://localhost:8000/admin` แล้วจะได้

.. image:: images/admin-entry.png

9. อ่านข้อมูลจากฐานข้อมูล

แก้ไขไฟล์ `myapp/views.py`

.. code-block:: python

  from django.shortcuts import render
  from django.http import HttpResponse
  from .models import Entry

  def index(req):
      entries = Entry.objects.all()
      return render(req, 'myapp/index.html', { 'entries': entries })

10. ใช้ entries ใน `myapp/templates/myapp/index.html`

.. code-block:: html

  {% extends 'myapp/base.html' %}
  {% block content %}
  <div class="container">
    <div class="row">
      {% for entry in entries %}
        {% include 'myapp/_calendar_entry.html' %}
      {% endfor %}
    </div>
  </div>
  {% endblock %}

11. ใช้ entry ใน `myapp/templates/myapp/_calendar_entry.html`

.. code-block:: html

  <div class="calendar_entry col-lg-4">
    <br/>
    <h2>{{ entry.name }}</h2>
    <h4>{{ entry.date }}</h4>
    <p>
      {{ entry.description }}
    </p>
    <button class="btn btn-primary">ดูรายละเอียด</button>
  </div>

