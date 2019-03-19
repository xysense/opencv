## OpenCV: Open Source Computer Vision Library

### Resources

* Homepage: <https://opencv.org>
* Docs: <https://docs.opencv.org/master/>
* Q&A forum: <http://answers.opencv.org>
* Issue tracking: <https://github.com/opencv/opencv/issues>

### Contributing

Please read the [contribution guidelines](https://github.com/opencv/opencv/wiki/How_to_contribute) before starting work on a pull request.

#### Summary of the guidelines:

* One pull request per issue;
* Choose the right base branch;
* Include tests and documentation;
* Clean up "oops" commits before submitting;
* Follow the [coding style guide](https://github.com/opencv/opencv/wiki/Coding_Style_Guide).


#### Installing on a mac for XY Sense

Make a virtual env:

```virtualenv -p python3 cv```

Activate:

```source cv/bin/activate```

Install numpy:

```pip install numpy```
And pyyaml

```pip install pyyaml```

Run Cmake:

```
cd opencv
mdkir build
cd build
cmake -D CMAKE_BUILD_TYPE=DEBUG\
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
    -D PYTHON3_LIBRARY=`python -c 'import subprocess ; import sys ; s = subprocess.check_output("python-config --configdir", shell=True).decode("utf-8").strip() ; (M, m) = sys.version_info[:2] ; print("{}/libpython{}.{}.dylib".format(s, M, m))'` \
    -D PYTHON3_INCLUDE_DIR=`python -c 'import distutils.sysconfig as s; print(s.get_python_inc())'` \
    -D PYTHON3_EXECUTABLE=$VIRTUAL_ENV/bin/python \
    -D BUILD_opencv_python2=OFF \
    -D BUILD_opencv_python3=ON \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D ENABLE_CXX11=ON \
    -D ENABLE_PRECOMPILED_HEADERS=OFF \
    -D BUILD_EXAMPLES=OFF ..
```

compile:

```make -j4```

symbolic link opencv to your virtualenv:
```
# run this from where you ran cmake build
ln -s $PWD/lib/python3/cv2.cpython-37m-darwin.so $VIRTUAL_ENV/lib/python3.7/site-packages/cv2.so
```

Now verify that you've got opencv installed with your python:
```
$ python

>>> import cv2
>>> print(cv2.__version__)
>>> 4.0.1
```