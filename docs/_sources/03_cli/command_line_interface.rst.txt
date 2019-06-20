การใช้คำสั่งพื้นฐาน
=========================

คำสั่งพื้นฐานในการใช้งานบน terminal

กำหนดตำแหน่งทำงาน
----------------------

.. code-block:: sh

  # ติดตั้งคำสั่ง tree
  sudo apt-get install tree

  # แสดงรายการไฟล์และโฟล์เดอร์ในรูปแบบของต้นไม้
  tree 

  # แสดงตำแหน่งโฟล์เดอร์ที่ทำงานอยู่
  pwd

  # คำสั่งเปลี่ยนโฟล์เดอร์ทำงาน
  cd

  # คำสั่งแสดงรายการไฟล์
  ls


จัดการไฟล์และโฟล์เดอร์
----------------------------

.. code-block:: sh

  # Copy file
  cp 

  # Move file to new location 
  mv

  # Remove files
  rm

  # Make directory
  mkdir

  # Change mode
  chmod

  # Change owner
  chown


ข้อมูลระบบ
----------------------

.. code-block:: sh

  # Display system information
  df   free   uname  lsb_release

  # Display process information
  ps   top    

  # Display network information
  ifconfig    iwconfig

  # Display hardware information
  lshal   lshw   lspci   lsusb

ไฟล์ข้อความ
-------------------------

.. code-block:: sh

  # Find files
  find

  # Search content of text files
  grep    

  # Search and replace text files
  sed

  # Edit text file
  nano

  # Display file content
  cat    less    more


จัดการผู้ใช้และกลุ่ม
--------------------

.. code-block:: sh

  # Show user information
  who   whoami   groups   

  # Edit user
  adduser  deluser  passwd  usermod      

  # Edit group
  addgroup   delgroup


ขอความช่วยเหลือ
--------------------

.. code-block:: sh

  # Help commands 
  man     apropos    type    where  

  # Read manual
  arrow keys

  # Quit manual
  q

  # Flag
  man -k   # apropos  
  man -f   # search by title

  
