# 1import cv2
import numpy as np
import inutils
import easyocr
from matplotlib import pylab as pl

img=cv2.imread("")
gray=cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

pl.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
pl.show()

cont=cv2.findContours(edges.copy(), cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
cont=imutils.grab_contours(cont)
cont=sorted(cont, key=cv2.contourArea, reverse=True)[:8]

pos=None

for c in cont:
    approx=cv2.approcPolyDP(c,10,true)

    if len(approx)==4:
        pos=approx
        break

mask=np.zeros(gray.shape, np.uint8)
new_img=cv2.drawContours(mask, [pos], 0, 255, -1)
bitwise_img=cv2.bitwise_and(img, img, mask=mask)

(x,y)=np.where(mask==255)
(x1,y1)=(np.min(x), np.min(y))
(x2,y2)=(np.max(x), np.max(y))
cropp=gray[x1:x2, y1:y2]



pl.imshow(cv2.cvtColor(cropp, cv2.COLOR_BGR2RGB))
pl.show()
