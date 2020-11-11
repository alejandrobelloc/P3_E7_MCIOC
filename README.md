# Proyecto 3 - Entrega 7 - MCIOC // Grupo 4
Para la última entrega del curso, se debe predecir resultados a partir de la curva de hidratación de la tesis de Contreras.
En particular, se mostrarán las temperaturas en el tiempo de cada sensor y también la misma en cortes del centro modelo en los 3 planos (x,y,z). Luego de esto, se mostrará un gif animado con la evolución térmica a través del bloque de hormigón a estudiar. 

Para la correcta solución de esto, se debió utilizar lo que se realizó para la entrega N°6, donde a través de dos softwares (Putty y Filezilla) se busca correr los programas y obtener los parámetros que se pedían. 

# **Aviso importante**
**Sin embargo, surgió un problema al intentar correr el programa a través de Putty, dado que al ingresar con la contraseña de nuestro grupo (4), este no dejaba abrir el cluster y se cerraba automáticamente el programa, por lo cual no se pudo obtener lo que se pedía para la entrega. No obstante, igualmente se observarán a continuación, algunos de los gráficos anteriormente mencionados, además de los códigos para correr en Python o algún otro software lo pedido.**

<br>

# Informe

### Paso a 3D

Para pasar a 3D, se añadieron los parametros que se presentan a continuación.
- "c" que corresponde a la profundidad
- "Nz" que corresponde al numero de intervalos en z
Mientras que en u_k y u_km1 se añadió Nz+1 para dejar los arreglos en tres dimensiones y dentro del loop en el espacio se añadió un for correspondiente al eje z.
Con esto el Laplaciano quedó de la siguiente forma
- nabla_u_k = (u_k[i-1,j,m] + u_k[i+1,j,m] + u_k[i,j-1,m] + u_k[i,j+1,m] + u_k[i,j,m-1] + u_k[i,j,m+1] -6*u_k[i,j,m])
           
 Con lo que finalmente, el Forward Euler que se le agregó el calor de hidratación (archivo .py que se nos fue entregado) quedó de la siguiente forma
- u_km1[i,j,m] = u_k[i,j,m] + alpha*nabla_u_k + Calor_de_hidratacion(t,DC)*dt


### Condiciones de Borde
- Utilizar condiciones de borde de gradiente cero para los lados del bloque (lados izquierdo, derecho, adelante, atrás y abajo del bloque)
- Utilizar la temperatura ambiental en la cara arriba del bloque. 
   - u_k[0,:,:] = u_k[1,:,:] + 0*dx      #borde delantero
   - u_k[-1,:,:] = u_k[-2,:,:] + 0*dx    #borde trasero
   - u_k[:,:,0] = u_k[:,:,1] + 0*dy      #borde izquierdo
   - u_k[:,:,-1] = u_k[:,:,-2] + 0*dy    #borde derecho
   - u_k[:,0,:] = ambiente               #borde superior
   - u_k[:,-1,:] = u_k[:,-2,:] + 0*dz    #borde inferior
   - Ambiente se sacó del archivo .cvs correspondiente a las temperaturas registradas en el sensor 14.

### Temperatura en el tiempo para cada sensor tanto predicha como registrada, cada sensor por separado
 
Para realizar esto se utilizó en primer lugar el codigo que se encuentra adjunto en esta entrega llamado "caso3d.py" donde se reutilizó el codigo entregado en el enunciado llamado "graficar.py" donde se pasaban los datos disponibles en el archivo .csv para poder graficar los diferentes sensores para el caso 1 - camara de curado. Luego por cada sensor se creo un array donde se fueron guardando los datos correspondientes al sensor, los que se sacaron de u_k en la posicion redondeada del sensor (esto debido a que algunos puntos no se encontraban en el arreglo).
Finalmente, se creó un codigo que recorria ambas listas de arreglos e iba graficando la temperatura en el tiempo para cada sensor ya sea la predicha como la registrada.
