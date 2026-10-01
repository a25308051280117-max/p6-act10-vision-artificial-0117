# p6-act10-vision-artificial-0117
vision artificial
import numpy as np
import cv2

# vision artificial act10 NC 0117

# Lee la imagen
img = cv2.imread("carro.jpg")

# Verifica que la imagen exista
if img is None:
    print("No se encontro carro.jpg")
    exit()

# Muestra la imagen original
cv2.imshow("carro.jpg", img)
cv2.waitKey(0)
cv2.destroyAllWindows()


#linea
print("-------------------------------------")

# Lee nuevamente la imagen
img = cv2.imread("carro.jpg")

# Dibuja una diagonal blanca de 3px
img = cv2.line(img,(0,0),(img.shape[1]-1,img.shape[0]-1),
               (255,255,255),3)

# Abre la ventana con la imagen
cv2.imshow("carro.jpg", img)
cv2.waitKey(0)
cv2.destroyAllWindows()


#el circulo
print("el circulo 0117")

# Lee nuevamente la imagen
img = cv2.imread("carro.jpg")

# Obtiene el centro de la imagen
x = img.shape[1] // 2
y = img.shape[0] // 2

# Dibuja un circulo azul de radio 10px
img = cv2.circle(img, (x,y), 10, (255,0,0),-1)

# Abre la ventana con la imagen
cv2.imshow("carro.jpg", img)
cv2.waitKey(0)
cv2.destroyAllWindows()


#el texto
print("el texto 0117")

# Lee nuevamente la imagen
img = cv2.imread("carro.jpg")

# Añade a la imagen el texto
img = cv2.putText(img, "Example Text", (20, 40),
                  cv2.FONT_HERSHEY_SIMPLEX,
                  0.8, (255, 255, 255), 2)

# Abre la ventana con la imagen
cv2.imshow("carro.jpg", img)
cv2.waitKey(0)
cv2.destroyAllWindows()


# Esta funcion agrega un punto en el lugar donde se hace click
def setPoint(event,x,y,flags,param):
    if event == cv2.EVENT_LBUTTONUP:
        cv2.circle(img, (x, y), 3, (255, 255, 255),-1)


# Lee la imagen del carro
img = cv2.imread("carro.jpg")

# Nombramos la ventana y asignamos el setMouseCallback
cv2.namedWindow('frame1')
cv2.setMouseCallback('frame1',setPoint)

while True:
    cv2.imshow('frame1',img)

    if cv2.waitKey(1) & 0xFF == 27:
        break

# Cerramos la ventana
cv2.destroyAllWindows()


# Trackbars

def on_trackbar(val):
    print(val)

# Lee la imagen del carro
img = cv2.imread("carro.jpg")

# Crea la ventana
cv2.namedWindow('frame')

# Crea tres trackbar en frame
cv2.createTrackbar('R','frame',0,255,on_trackbar)
cv2.createTrackbar('G','frame',0,255,on_trackbar)
cv2.createTrackbar('B','frame',0,255,on_trackbar)

while True:

    # Obtiene las posiciones de los trackbars
    r = cv2.getTrackbarPos('R','frame')
    g = cv2.getTrackbarPos('G','frame')
    b = cv2.getTrackbarPos('B','frame')

    # Aplica el color seleccionado sobre la imagen
    color = np.zeros_like(img)
    color[:] = [b,g,r]

    # Combina la imagen del carro con el color
    resultado = cv2.addWeighted(img, 0.7, color, 0.3, 0)

    cv2.imshow('frame',resultado)

    k = cv2.waitKey(1) & 0xFF

    if k == 27:
        break

cv2.destroyAllWindows()

img = cv2.imread("carro.jpg")

x = 0
y = 0
moviendo = False

def mover(event, mx, my, flags, param):
    global x, y, moviendo

    if event == cv2.EVENT_LBUTTONDOWN:
        moviendo = True

    elif event == cv2.EVENT_MOUSEMOVE and moviendo:
        x = mx - img.shape[1] // 2
        y = my - img.shape[0] // 2

    elif event == cv2.EVENT_LBUTTONUP:
        moviendo = False

cv2.namedWindow("carro")
cv2.setMouseCallback("carro", mover)

while True:
    fondo = np.zeros((600, 800, 3), np.uint8)

    # Coloca el carro en la posición del mouse
    alto, ancho = img.shape[:2]

    # Evita que se salga de la ventana
    x2 = max(0, min(x, 800 - ancho))
    y2 = max(0, min(y, 600 - alto))

    fondo[y2:y2+alto, x2:x2+ancho] = img

    cv2.imshow("carro", fondo)

    if cv2.waitKey(1) & 0xFF == 27:
        break

cv2.destroyAllWindows()
