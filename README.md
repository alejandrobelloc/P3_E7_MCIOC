# P3_E7_MCIOC
Para la última entrega del curso, se debe predecir resultados a partir de la curva de hidratación de la tesis de Contreras.
En particular, se mostrarán las temperaturas en el tiempo de cada sensor y también la misma en cortes del centro modelo en los 3 planos (x,y,z). Luego de esto, se mostrará un gif animado con la evolución térmica a través del bloque de hormigón a estudiar. 

Para la correcta solución de esto, se debió utilizar lo que se realizó para la entrega N°6, donde a través de dos softwares (Putty y Filezilla) se busca correr los programas y obtener los parámetros que se pedían. 

# **Aviso importante**
**Sin embargo, surgió un problema al intentar correr el programa a través de Putty, dado que al ingresar con la contraseña de nuestro grupo (4), este no dejaba abrir el cluster y se cerraba automáticamente el programa, por lo cual no se pudo obtener lo que se pedía para la entrega. No obstante, igualmente se observarán a continuación, algunos de los gráficos anteriormente mencionados, además de los códigos para correr en Python o algún otro software lo pedido.**

<br>


### Condiciones de Borde
- Utilizar condiciones de borde de gradiente cero para los lados del bloque (lados izquierdo, derecho, adelante, atrás y abajo del bloque)
- Utilizar la temperatura ambiental en la cara arriba del bloque. 

<br>

    - u_k[0,:,:] = u_k[1,:,:] + 0*dx      #borde delantero
    - u_k[-1,:,:] = u_k[-2,:,:] + 0*dx    #borde trasero
    - u_k[:,:,0] = u_k[:,:,1] + 0*dy      #borde izquierdo
    - u_k[:,:,-1] = u_k[:,:,-2] + 0*dy    #borde derecho
    - u_k[:,0,:] = ambiente               #borde superior
    - u_k[:,-1,:] = u_k[:,-2,:] + 0*dz    #borde inferior
    - Ambiente se sacó del archivo .cvs correspondiente a las temperaturas registradas en el sensor 14.

 
