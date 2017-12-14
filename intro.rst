introduce
========================================
 
 **good good study ,day day up !**
 
 *good good study ,day day up !*
 
 ``good good study ,day day up !``
 
.. _my-reference-label:

 *good good study ,day day up !*:subscript:`oMygod`
 
 *good good study ,day day up !*:superscript:`oMygod`
 
 :title-reference:`good good study ,day day up !`

 
* one
* two
  three
  
 * onechild
 * twochild

#. one
#. two 

  | one
  | two
  


read the docs
-----------------

refer
^^^^^^^^^
    https://readthedocs.org/
    http://www.sphinx-doc.org/en/stable/rest.html
    http://www.jianshu.com/p/78e9e1b8553a
    https://zh-sphinx-doc.readthedocs.io/en/latest/contents.html

install
^^^^^^^^^^^
#. apt install build-essential
#. apt install python-dev
#. apt install python-pip
#. apt install python-setuptools
#. apt install libxml2-dev
#. apt install libxslt1-dev
#. apt install zlib1g-dev
#. apt install elasticsearch
#. apt install redis-server
#. pip install virtualenv
#. virtualenv rtd && cd rtd
#. source bin/activate
#. apt install git
#. git clone https://github.com/rtfd/readthedocs.org.git
#. cd readthedocs.org
#. pip install -r requirements.txt
#. python manage.py migrate
#. python manage.py collectstatic
#. python manage.py loaddata test_data
#. python manage.py runserver 0.0.0.0:8000
#. apt install texlive-latex-recommended
#. apt install texlive-fonts-recommended
#. apt install texlive-latex-extra
#. apt install latexmk 
#. make latexpdf LATEXMKOPTS="-silent"

usage 
^^^^^^^^^^^^
* install Sphinx ::

    apt install python-pip -y
    pip install sphinx sphinx-autobuild
    pip install --upgrade pip 安装最新版pip
    mkdir doc && cd doc
    sphinx-quickstart
    make html


    
