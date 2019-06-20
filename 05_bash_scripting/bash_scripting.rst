การเขียนคำสั่ง Bash
======================

การใช้คำสั่งภาษา Bash

Introduction
-----------------

1. Open terminal :  gnome- terminal, konsole

2. What’s this?  mkdir -p 1104154/scripting; cd 1104154/scripting

3. Two ways to say hello

  3.1. interactive (live) scripting: type command at the prompt

  .. code-block:: sh

     echo ‘hello world’

  3.2. non-interactive: 

    * create file .sh 

    .. code-block:: sh

      vi hello.sh

      gedit hello.sh

    * put command in the file 

    * save 

    * execute it 

    .. code-block:: sh

      chmod +x hello.sh

      ./hello.sh

4. What’s your shell?

5. Pick your editor : vi, nano

6. Fast fingers

Variables
------------

1. Refers to data in memory: VARNAME=value

  .. code-block:: sh

    age=29
    name='Paul Phoenix'
    name="Angelina Jolie"

2. Access variable value: $VARNAME or ${VARNAME}

  .. code-block:: sh

   echo $age
   echo $name

3. Reading value from keyboard: read VARNAME

  .. code-block:: sh

    read age
    echo $age

4. Ready to use variables on your shell: printenv

5. Arithmetic operations

  .. code-block:: sh

    z=`echo $x + $y | bc`

    # +,   -,   ++,   --,   *,   /,   %,  ^
    # !,  &&, ||,   >,   >=,   <,   <=,  ==, !=

    z=`expr $x + $y`

    # |,  &,  <,  <=,  =,  !=,  >=,  >,  +,  -,  \*,  /,  % 

    z=$(( x + y ))

    # +,   -,   ++,   --,   *,   /,   %,  **


If/Else
-----------

1. One-way

  .. code-block:: sh

    if [ $x -eq $y ]; then
      echo "x == y"
    fi

2. Two-way

  .. code-block:: sh

    if [ $x -le $y ]; then
      echo "x <= y"
    else
      echo "x > y"
    fi

3. Multi-way

  .. code-block:: sh

    if [ $x -eq $y ]; then
      echo "x == y"
    elif (( x > 20 )); then
      echo "x > 20"
    elif [ -f /bin/sh ] && [ -x /bin/sh ]; then
      echo "you’ve got shell" 
    else
      echo 'hmmmmmmmm'
      echo 'what do I do now?'
    fi

4. Operators

  * Condition Expression with binary operators

  .. code-block:: sh

    [ $a  operator  $b ]

    # -eq ,-ne, -lt, -le, -gt, -ge  

  * Condition Expression with unary operators

  .. code-block:: sh

    [ operator $a ]

    # -s, -f, -d, -x, -w, -r

  * Logical operators

  .. code-block:: sh

   ConditionExpression operator ConditionExpression

   # &&, ||


Looping
------------

for
-----

.. code-block:: sh

  for i in array
  do
    statements
    statements
  done

.. code-block:: sh

  read numbers
  for i in number 
  do  
    echo “i = $i”
  done

.. code-block:: sh

  read n
  for((i=0; i<=$n; i++)) do 
    echo “i = $i”
  done


while
-------

.. code-block:: sh

  while condition
  do
    statements
    statements
  done

.. code-block:: sh

  i=0
  while [ $i -lt 10 ]
  do
    i=`expr $i + 1`
    echo “i = $i”
  done

.. code-block:: sh

  i=0
  while((i < 10))
  do
    ((i++))
    echo “i = $i”
  done


Cases
------

.. code-block:: sh

  case $var in
    a) statements ;;
    b) statements ;;

    *) statments ;;
  esac

.. code-block:: sh

  read grade
  case $grade in
  4) echo "best" ;;
  3) echo "good" ;;
  2) echo "okay" ;;
  1) echo "try harder" ;;
  0) echo "fail" ;;
  *) echo "wrong input" ;;
  esac


Functions
-----------

.. code-block:: sh

  functionname()
  {
  statements
    statements
  }

  functionname
  functionname 1 2 3 ...

.. code-block:: sh

  fac()
  {
    if [ "$1" -gt 1 ]
       then
      n=`expr $1 - 1`
      r=`fac $n`
      result=`expr $1 \* $r`
      echo $result
    else
      echo 1
    fi
  }

  echo "Enter a number: "
  read n
  echo "$n! = `fac $n`"


Files
----------

.. code-block:: sh

  show()
  {
  case $1 in
      
      -c) cat $1 ;;
      -g) grep -e $2 $1 ;;
      -h) head $1 ;;
      -s) sed -i '/$2/$3' $1 ;;
  esac
  }

  show -c users.txt
  show -g users.txt Paul
  show -s users.txt Paul Nina


Search & Sort
---------------

1. $RANDOM

.. code-block:: sh

  echo $RANDOM $(( RANDOM % 6 ))

2. awk 

.. code-block:: sh

  awk '$1 >20000' salary.txt

3. sort

.. code-block:: sh

  sort -n filename

4. seq 

.. code-block:: sh

  seq 0 2 10

5. printf

.. code-block:: sh

  printf "format" values

6. uniq = sort -u

.. code-block:: sh

  uniq filename


Advanced
-----------

1. Bash Array

.. code-block:: sh

  a=(10 30 20 30 50 40)
  u=( ${a[@]} )
  echo ${a[0]}            # 10
  echo ${a[*]}            # 10 30 20 30 50 40
  echo ${a[@]}            # 10 30 20 30 50 40
  echo ${#a[@]}           # 6
  echo ${#a}              # 2   #number of characters in a[0] 
  echo ${a[@]:2:3}        # 20 30 50
  echo ${a[@]/30/15}      # 10 15 20 15 50 40


2. Bash for

.. code-block:: sh

  a=(10 30 20 30 50 40)
  for (( i=0; i<5; i++ ))
  do
    printf "%d = %d\n" $i ${a[$i]}
  done

3. Bash string

.. code-block:: sh

  ${#string}            # length of $string
    
  ${string:pos}         # extract substring from $string at $pos
  ${string:pos:length}  # extract substring from $pos to $pos+$length

  ${string#term}        # strip shortest $term from front 
  ${string##term}       # strip longest $term from front
  ${string%term}        # strip shortest $term from back
  ${string%%term}       # strip longest $term from back

  ${string/old/new}     # replace first match of $old with $new
  ${string//old/new}    # replace all matches of $old with $new
  ${string/#old/new}    # if $old matches front of $string replace it 
  ${string/%old/new}    # if $old matches end of $string replace it

