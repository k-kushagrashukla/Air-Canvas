# Air Canvas
 A virtual drawing tool that allows you to draw in the air using hand gestures.
 
## Highlights
-Used OpenCV to capture live video from webcam

-Used MediaPipe for hand tracking and for gesture detection

-Used Deque for fast and efficient data storing

## Explanation (line by line explanation of every code)

```python
import cv2
import numpy as np
import mediapipe as mp
from collection import deque
```
cv2: Open library, image processing ke liye.

numpy: mathematical operation aur array ke liye

mediapipe: handtracking aur landmarks ko detect karne ke liye

deque: data structure jo painting ke points ko store karega

```python
bpoints=[deque(maxlen=1024)]
gpoints=[deque(maxlen=1024)]
rpoints=[deque(maxlen=1024)]
ypoints=[deque(maxlen=1024)]
```
har color ke liye ek deque banaya gya hai , taaki vo drawing points store kar sake

```python
colors=[(255,0,0),(0,255,0),(0,0,255),(0,255,255)]
colorIndex=0
```
RGB values ke through color define kiye gye hai, aur colorIndex selected color ko detect karega.

```python
paintWindow=np.zeros((471,636,3)) + 255
```
Ek blank white paint window banayi gyi hai (471*636 pixels)

```python
paintWindow=cv2.rectangle(paintWindow,(40,1),(140,65),(0,0,0),2)
paintWindow=cv2.rectangle(paintWindow,(160,1),(255,65),(255,0,0),2)
paintWindow=cv2.rectangle(paintWindow,(275,1),(370,65),(0,255,0),2)
paintWindow=cv2.rectangle(paintWindow,(390,1),(485,65),(0,0,255),2)
paintWindow=cv2.rectangle(paintWindow,(505,1),(600,65),(0,255,255),2)

cv2.putText(paintWindow,"CLEAR",(49,33),cv2.FONT_HERSHEY_COMPLEX,0.5,(0,0,0),2,cv2.LINE_AA)
cv2.putText(paintWindow,"BLUE",(185,33),cv2.FONT_HERSHEY_COMPLEX,0.5,(0,0,0),2,cv2.LINE_AA)
cv2.putText(paintWindow,"GREEN",(298,33),cv2.FONT_HERSHEY_COMPLEX,0.5,(0,0,0),2,cv2.LINE_AA)
cv2.putText(paintWindow,"RED",(420,33),cv2.FONT_HERSHEY_COMPLEX,0.5,(0,0,0),2,cv2.LINE_AA)
cv2.putText(paintWindow,"YELLOW",(520,33),cv2.FONT_HERSHEY_COMPLEX,0.5,(0,0,0),2,cv2.LINE_AA)
```
Clear aur color buttons banaye gye hai , widnow top par

```python
cv2.namedWindow('paint',cv2.WINDOW_AUTOSIZE)
```
paintwindow ko display karne ke liye ek opencv window banayi gyi hai

```python
mpHands=mp.solutions.hands
hands=mpHands.Hands(max_num_hands=1,min_detection_confidence=0.7)
mpDraw=mp.solutions.drawing_utils
```
sirf ek haath detect karne ke liye (max_num_hands=1)
minimum_detection_confidence 0.7 set ki gyi hai
landmarks draw karne ke liye mpdraw

