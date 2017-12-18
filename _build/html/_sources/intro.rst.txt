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
#. two我是一个ingnew

  | one
  | two
  
.. image:: images/c0d.png

.. list-table:: Frozen Delights!
   :widths: 15 10 30
   :header-rows: 1

   * - Treat
     - Quantity
     - Description
   * - Albatross
     - 2.99
     - On a stick!
   * - Crunchy Frog
     - 1.49
     - If we took the bones out, it wouldn't be
       crunchy, now would it?
   * - Gannet Ripple
     - 1.99
     - On a stick!

read the docs
-----------------

refer
^^^^^^^^^
.. seealso::
   | `readthedocs官方网址 <https://readthedocs.org/>`_
   | `sphinx语法文档 <http://www.sphinx-doc.org/en/stable/rest.html>`_
   | `个人博客文档 <http://www.jianshu.com/p/78e9e1b8553a>`_
   | `sphinx中文语法文档 <https://zh-sphinx-doc.readthedocs.io/en/latest/contents.html>`_

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
#. apt install texlive-xetex
#. apt install latex-cjk-all

usage 
^^^^^^^^^^^^
* install Sphinx ::

    apt install python-pip -y
    pip install sphinx sphinx-autobuild
    pip install --upgrade pip 安装最新版pip
    mkdir doc && cd doc
    sphinx-quickstart
    make html

* conf.py
    latex_engine=xelatex 解决无法生成pdf问题
    texhash 不知道干啥用的
    'preamble': '''
        \usepackage{xeCJK} 解决无法显示中文的问题
    '''
    

    
