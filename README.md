# Tarea para BD05.
## Detalles de la tarea de esta unidad.

Antes de empezar a realizar los ejercicios debes crear las tablas necesarias. Para ello debes utilizar el archivo BD05_CreaTablasTarea.sql(0.01 MB) y en Archivos de Comandos SQL debes cargarlo y ejecutarlo.

Inserta un registro nuevo en la tabla PROFESORADO utilizando la herramienta gráfica Application Express que ofrece Oracle Database Express. Los datos deben ser los siguientes: 
Codigo: 1
Nombre: NURIA
Apellidos: ANERO GONZALEZ
DNI: 58328033X
Especialidad: MATEMATICAS
Fecha_Nac: 22/02/1972
Antiguedad: 9
Debes entregar una captura de pantalla de la ventana en la que estás introduciendo los datos, justo antes de pulsar el botón para guardarlos.  
![image](https://user-images.githubusercontent.com/44543081/54458549-8bd7fb00-4764-11e9-92a1-74f2bac46ed9.png)  
![image](https://user-images.githubusercontent.com/44543081/54458641-c5106b00-4764-11e9-8899-432fdfe75a16.png)  
Inserta varios registros más en la tabla PROFESORADO utilizando sentencias SQL. En la entrega de la tarea debes copiar las sentencias que has utilizado. Los datos deben ser los siguientes: 
Tabla PROFESORADO
Codigo	Nombre	Apellidos	DNI	Especialidad	Fecha_Nac	Antiguedad
2	MARIA LUISA	FABRE BERDUN	51083099F	TECNOLOGIA	31/03/1975	4
3	JAVIER	JIMENEZ HERNANDO		LENGUA	04/05/1969	10
4	ESTEFANIA	FERNANDEZ MARTINEZ	19964324W	INGLES	22/06/1973	5
5	JOSE M.	ANERO PAYAN				
Los datos que aparecen en blanco no deben utilizarse en las sentencias.
```SQL
INSERT INTO PROFESORADO (CODIGO, NOMBRE, APELLIDOS, DNI, ESPECIALIDAD,FECHA_NAC, ANTIGUEDAD) VALUES 
(2, 'MARIA LUISA', 'FABRE BERDUN', '51083099F', 'TECNOLOGIA', '03/31/1975', 4);
INSERT INTO PROFESORADO (CODIGO, NOMBRE, APELLIDOS, ESPECIALIDAD,FECHA_NAC, ANTIGUEDAD) VALUES 
(3, 'JAVIER', 'JIMENEZ HERNANDO', 'LENGUA', '05/04/1969', 10);
INSERT INTO PROFESORADO (CODIGO, NOMBRE, APELLIDOS, DNI, ESPECIALIDAD,FECHA_NAC, ANTIGUEDAD) VALUES 
(4, 'ESTEFANIA', 'FERNANDEZ MARTINEZ', '19964324W', 'INGLES', '06/22/1973', 5);
INSERT INTO PROFESORADO (CODIGO, NOMBRE, APELLIDOS) VALUES 
(5, 'JOSE M.', 'ANERO PAYAN');
```
Modifica los registros de la tabla CURSOS para asignar a cada curso un profesor o profesora. Utiliza para ello la herramienta gráfica, entregando con la tarea una captura de pantalla de la pestaña Datos de esa tabla, donde se aprecien todos los cambios que has realizado. El profesorado que debes asignar a cada curso es: 
Tabla CURSOS
Codigo	Cod_Profe
1	4
2	2
3	2
4	1
5	1
6	3  
![image](https://user-images.githubusercontent.com/44543081/54458685-e5402a00-4764-11e9-90a3-930dd98f10d1.png)  
![image](https://user-images.githubusercontent.com/44543081/54458713-f25d1900-4764-11e9-9153-fab147c2c684.png)  
![image](https://user-images.githubusercontent.com/44543081/54458741-03a62580-4765-11e9-92b4-f5e77706c85b.png)  

Modifica el registro de la profesora "ESTEFANIA", usando sentencias SQL, y cambia su fecha de nacimiento a "22/06/1974" y la antigüedad a 4. En la entrega de la tarea debes copiar la sentencia que has utilizado.
```SQL
UPDATE PROFESORADO SET FECHA_NAC='06/22/1974', ANTIGUEDAD=4 WHERE NOMBRE ='ESTEFANIA';
```
Modifica las antigüedades de todos los profesores y profesoras incrementándolas en 1 en todos los registros. Debes hacerlo usando un sola sentencia SQL que debes copiar para la entrega de la tarea.
```SQL
UPDATE PROFESORADO SET ANTIGUEDAD=ANTIGUEDAD+1;
```
Elimina, de la tabla CURSOS, el registro del curso que tiene el código 6. Debes realizar esta acción desde la herramienta gráfica. Debes entregar una captura de pantalla de la ventana en la que vas a borrar el registro, justo antes de pulsar el botón Aceptar para confirmar el borrado.  
![image](https://user-images.githubusercontent.com/44543081/54458828-394b0e80-4765-11e9-884d-3c0ad18a1bb7.png)  
Elimina, de la tabla ALUMNADO, aquellos registros asociados al curso con código 3. Debes hacerlo usando un sola sentencia SQL que debes copiar para la entrega de la tarea.
```SQL
DELETE FROM ALUMNADO WHERE COD_CURSO=3;
```
Inserta los registros de la tabla ALUMNADO_NUEVO en la tabla ALUMNADO. Debes hacerlo usando un sola sentencia SQL que debes copiar para la entrega de la tarea.
```SQL
INSERT INTO ALUMNADO (Nombre,Apellidos,Sexo,Fecha_Nac) SELECT Nombre,Apellidos,Sexo,Fecha_Nac FROM ALUMNADO_NUEVO;
```
En la tabla CURSOS, actualiza el campo Max_Alumn del registro del curso con código 2, asignándole el valor correspondiente al número total de alumnos y alumnas que hay en la tabla ALUMNADO y que tienen asignado ese mismo curso.
```SQL
UPDATE CURSOS SET MAX_ALUMN=(SELECT COUNT(NOMBRE) FROM ALUMNADO) WHERE CODIGO=2;
```
Elimina de la tabla ALUMNADO todos los registros asociados a los cursos que imparte la profesora cuyo nombre es "NURIA".
```SQL
DELETE FROM ALUMNADO WHERE CODIGO=
(SELECT AL.CODIGO FROM ALUMNADO AL 
INNER JOIN CURSOS CU ON AL.COD_CURSO=CU.CODIGO 
INNER JOIN PROFESORADO PR ON CU.COD_PROFE=PR.CODIGO 
WHERE PR.NOMBRE='NURIA');
```
