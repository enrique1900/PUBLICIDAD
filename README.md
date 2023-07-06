# PUBLICIDAD

import numpy as np                     # Aqui importamos las librerias para la aleatoriedad
import matplotlib.pyplot as plt        # & Graficas

cL = [100, 0, 0, 0]                     #definimos la lista de la poblacion
averageList = [100, 0, 0, 0]            #definimos la lista con la poblacion en su estado inicial donde guardaremos las entradas
for i in range (30):                    #le decimos cuantas veces hara la simulacion
    if(cL[0] == 0):                     #los if, elif y else en este rango son condiciones de la poblacion
        x = np.random.choice([1, 2, 3, 4], 30, p = [0.63, 0.17, 0.13, 0.07])	
        for element in x:               #aqui asignamos las probabilidades del evento para un for de 30
            if((element == 2) and (cL[1] != 0)):
                cL[1] = cL[1] - 1
                cL[0] = cL[0] + 1
            elif((element == 3) and (cL[2] != 0)):
                cL[2] = cL[2] - 1
                cL[0] = cL[0] + 1
            elif((element == 4) and (cL[3] != 0)):
                cL[3] = cL[3] - 1
                cL[0] = cL[0] + 1
            else:
                cL[0] = cL[0]          # solo va contando la gente que deja de ser afectada
        for t in range(4):
            averageList.append(cL[t])  # añade a la lista de todos los resultados de poblaciones al acabar el for
    elif(cL[0] == 100):                # checa condiciones donde tecnicamente aqui empieza
        x = np.random.choice([1, 2, 3, 4], 30, p = [0.57, 0.20, 0.13, 0.10])
        for element in x:
            if(element == 1):
                cL[0] = cL[0]
            elif(element == 2):
                cL[1] = cL[1] + 1
                cL[0] = cL[0] - 1
            elif(element == 3):
                cL[2] = cL[2] + 1
                cL[0] = cL[0] - 1
            else:
                cL[3] = cL[3] + 1
                cL[0] = cL[0] - 1
            if(cL[0] == 0):         # esta parte sale del for si ve que ya no puede haber poblacion que se vea afectada
                break
            else:
                cL[0] = cL[0]
        for t in range(4):
            averageList.append(cL[t])
    else:                           #aqui eligira si sacar o agregar a alguien a los afectados
        x = np.random.choice([1, 2], 30, p = [0.50, 0.50])
        for element in x:
            if(element == 1):       #repite cosas de casos pasados
                x = np.random.choice([1, 2, 3, 4], p = [0.63, 0.17, 0.13, 0.07])
                if((element == 2) and (cL[1] != 0)):
                    cL[1] = cL[1] - 1
                    cL[0] = cL[0] + 1
                elif((element == 3) and (cL[2] != 0)):
                    cL[2] = cL[2] - 1
                    cL[0] = cL[0] + 1
                elif((element == 4) and (cL[3] != 0)):
                    cL[3] = cL[3] - 1
                    cL[0] = cL[0] + 1
                else:
                    cL[0] = cL[0]
            else:
                x = np.random.choice([1, 2, 3, 4], p = [0.57, 0.20, 0.13, 0.10])
                if(element == 1):
                    cL[0] = cL[0]
                elif((element == 2) and (cL[0] > 0)):
                    cL[1] = cL[1] + 1
                    cL[0] = cL[0] - 1
                elif((element == 3) and (cL[0] > 0)):
                    cL[2] = cL[2] + 1
                    cL[0] = cL[0] - 1
                elif((element == 4) and (cL[0] > 0)):
                    cL[3] = cL[3] + 1
                    cL[0] = cL[0] - 1
                else:
                    cL[0] = cL[0]
                if(cL[0] == 0):
                    break
                else:
                    cL[0] = cL[0]
        for t in range(4):
            averageList.append(cL[t])


print(averageList)               #Es nuestra lista final con su longitud
print(len(averageList))


v = 0                           #Graficas de cada una de las 4 categorias en orden
for f in range(0,31):
    v = 4*f
    plt.plot(f,[averageList[v]],"bo")
    if f > 0:
        plt.plot([f-1,f],[averageList[aux],averageList[v]],"g-")
    aux=v
plt.grid(True)
plt.xlabel("X")
plt.ylabel("Y")
plt.show()


v = 0
for f in range(0,31):
    v = ((4*f)+1)
    plt.plot(f,[averageList[v]],"bo")
    if f > 0:
        plt.plot([f-1,f],[averageList[aux],averageList[v]],"g-")
    aux=v
plt.grid(True)
plt.xlabel("X")
plt.ylabel("Y")
plt.show()


v = 0
for f in range(0,31):
    v = ((4*f)+2)
    plt.plot(f,[averageList[v]],"bo")
    if f > 0:
        plt.plot([f-1,f],[averageList[aux],averageList[v]],"g-")
    aux=v
plt.grid(True)
plt.xlabel("X")
plt.ylabel("Y")
plt.show()


v = 0
for f in range(0,31):
    v = ((4*f)+3)
    plt.plot(f,[averageList[v]],"bo")
    if f > 0:
        plt.plot([f-1,f],[averageList[aux],averageList[v]],"g-")
    aux=v
plt.grid(True)
plt.xlabel("X")
plt.ylabel("Y")
plt.show()


A lo largo del programa se declara el estado inicial de la poblacion con 100 personas no afectadas por la publicidad y tras la primer iteracion, 
se van afectando las personas por los distintos tipos de publicidad, que son: pagada, propia o ganada 
y colocandolas a lo largo de la lista "cL" con un max de 100 distribuidas entre todas. 
Mas tarde tras terminar de hacer la simulacion nos devuelve como fue su comportamiento a lo largo del tiempo en 4 graficas diferentes.
