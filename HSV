import cv2
import numpy as np


def nothing(x):
    pass


cap = cv2.VideoCapture(0)

cv2.namedWindow("WebcamX Mask")

cv2.createTrackbar("Lower-H", "WebcamX Mask", 0, 180, nothing)
cv2.createTrackbar("Lower-S", "WebcamX Mask", 0, 255, nothing)
cv2.createTrackbar("Lower-V", "WebcamX Mask", 0, 255, nothing)

cv2.createTrackbar("Upper-H", "WebcamX Mask", 0, 180, nothing)
cv2.createTrackbar("Upper-S", "WebcamX Mask", 0, 255, nothing)
cv2.createTrackbar("Upper-V", "WebcamX Mask", 0, 255, nothing)

cv2.setTrackbarPos("Upper-H", "WebcamX Mask", 180)
cv2.setTrackbarPos("Upper-S", "WebcamX Mask", 255)
cv2.setTrackbarPos("Upper-V", "WebcamX Mask", 255)

while True:
    _, frame = cap.read()
    frame = cv2.flip(frame, 1)
    frame_hsv = cv2.cvtColor(frame, cv2.COLOR_BGR2HSV)

    lower_h = cv2.getTrackbarPos("Lower-H", "WebcamX Mask")
    lower_s = cv2.getTrackbarPos("Lower-S", "WebcamX Mask")
    lower_v = cv2.getTrackbarPos("Lower-V", "WebcamX Mask")

    upper_h = cv2.getTrackbarPos("Upper-H", "WebcamX Mask")
    upper_s = cv2.getTrackbarPos("Upper-S", "WebcamX Mask")
    upper_v = cv2.getTrackbarPos("Upper-V", "WebcamX Mask")

    lower_color = np.array([lower_h, lower_s, lower_v])
    upper_color = np.array([upper_h, upper_s, upper_v])

    mask = cv2.inRange(frame_hsv, lower_color, upper_color)
    bitwise =cv2.bitwise_and(frame, frame,  mask=mask)

    cv2.imshow("WebcamX", frame)
    cv2.imshow("WebcamX Mask", mask)
    cv2.imshow("bitwise", bitwise)

    if cv2.waitKey(1) & 0xFF == ord("q"):
        break

cap.release()
cv2.destroyAllWindows()
