# Examples #
## Exemple 1 ##
```
import scipy
import pylab
from zopencv import *
l=scipy.lena().astype(numpy.float32)
l2=l.copy()
cvLaplace(l,l2,3)
pylab.imshow(l2)
pylab.show()
```
## Exemple 2 ##
```
import numpy
import scipy
from zopencv import *
CV_VALUE=1
src=scipy.lena().astype(numpy.uint8)
## initialize default contour
length=int(50)
points=(numpy.vstack([scipy.cos(numpy.arange(0,scipy.pi*2,scipy.pi*2./length)),scipy.sin(numpy.arange(0,scipy.pi*2,scipy.pi*2./length))])*250+256).T.astype(numpy.int32)
## setup parameters
alpha=numpy.array([0.45], dtype=numpy.float32)
beta=numpy.array([0.1], dtype=numpy.float32)
gamma=numpy.array([0.45], dtype=numpy.float32)
size=cvSize(5,5)
criteria=CvTermCriteria()
criteria.type=CV_TERMCRIT_ITER+CV_TERMCRIT_EPS;
criteria.max_iter=1;
criteria.epsilon=0.0;
## simply display the result
cvNamedWindow("win1",1)
# run the system
for x in range(1000):
        cvSnakeImage( src, zopencv.memory_addr_of_numpy_array(points),length,alpha,beta, gamma,CV_VALUE,size,criteria,0 );
        # draw the resulting contour
        srcb=src.copy()
        for x in range(length-1):
                src_point=cvPoint(points[x,0],points[x,1])
                dst_point=cvPoint(points[x+1,0],points[x+1,1])
                color=cvScalar(255,0,0,0)
                cvLine( srcb,src_point, dst_point,color,1,8,0 )
        cvShowImage("win1",srcb)
        cvWaitKey(1000)
```