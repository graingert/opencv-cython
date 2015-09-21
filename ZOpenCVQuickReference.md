ZOpenCV is a wrapper for OpenCV in python.


---


It supports all the version of OpenCV.

There is **an almost complete support** of all the features of OpenCV with an easy interface.

---

## Building ZOpenCV ##

The basic line to build the wrapper :

```
ln -s /usr/bin/g++-4.1 g++
PATH=$PWD:$PATH ./build.sh
```

## Basics about ZOpenCV ##

start importing

```
import zopencv
```

All functions have **exactly the same prototype as their C prototype**, and for the moment
default argument are not supported, so you have to pass ALL THE ARGUMENTS !
(sorry for this)

Meaning that a function like
```

```

### So the key question is how do we create objects / pointers and all that stuffs ? ###

First of all, let's see how to create object.

You can create Object by using the Structure Name as a constructor :
```
myimage=zopencv.CvImage()
mypoint=zopencv.CvPoint()
```

You may of course use the OpenCv constructors when they exists :
```
mypoint=zopencv.cvPoint(0,0)
```

You can also create pointer on objects :

You can create Object by using the Structure Name as a constructor :
```
myimage=zopencv.zopencv_pclasses.PointerOnCvImage()
mypoint=zopencv.zopencv_pclasses.PointerOnCvPoint()
```

Of cource to avoid this complited scoping, when experimenting you'd rather do:
```
from zopencv import *
from zopencv.zopencv_pclasses import *
```

Note that, **as in C, it just creates the structure** and that no initialize procedure is called.

For pointers :

```
Well there are many ways :
* By directly passing an object or a pointer to an object of that type
* By using the "get_pointer" function on an object.
* numpy.arrays can be cast into pointer types for the basic types you may encounter :
  (float * , unsigned int * ,....).
   You have of course to create an array of the correct size before, else you are 
   going to segfault.
* just specify an int, with the right largeness according to your machine to give an explicit address
```

As syntaxic sugar, all function that take a specific object type as first argument are also available as method of this object. Hence, it gives a little "object" spice although
everything remains in "C".

### Special Casts ###

Note that when, Images and Matrices are required, you can always pass directly a numpy array, and a image handle will be created for it.