# **DjangoProject**
## **Proyecto de Python con Framework Django y base de datos SQLite**

EL sistema muesra el archivo CSV sacado de la fuente de internet https://www.stats.govt.nz/large-datasets/csv-files-for-download/

![imagen](https://github.com/Carlitos2823/DjangoProject/assets/107945651/586da051-f474-44f2-b879-3585814e2fa6)

Ademas a continuación se comparte el codigo para pasar desde el dataset CSV a una base de datos llamada libreria diseñada en SQLite

## **SCRIPT PARA PASAR DE UN CSV A UNA TABLA DE SQLITE**
import csv
import sqlite3

#Nombre del archivo CSV y nombre de la tabla SQLite
csv_filename = 'data.csv'
sqlite_db_filename = 'libreria.db'
#Conectarse a la base de datos SQLite
conn = sqlite3.connect(sqlite_db_filename)
cursor = conn.cursor()
#Abrir el archivo CSV y leer los datos
with open(csv_filename, 'r') as csv_file:
    csv_reader = csv.reader(csv_file)
    next(csv_reader)  #Para omitir la fila de encabezados si la tienes en el archivo CSV
    for row in csv_reader:
        #Insertar los datos en la tabla SQLite
        cursor.execute('''
            INSERT INTO libreria_dato ( Direction , Year, Date, Weekday, Country, Commodity, Transport_Mode, Measure, Value, Cumulative)
            VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
        ''', (row[0], row[1], row[2], row[3], row[4], row[5], row[6], row[7], row[8], row[9] ))  # Ajusta los índices según la estructura de tu CSV
#Guardar los cambios y cerrar la conexión a la base de datos
conn.commit()
conn.close()

## Problemas encontrados al desarrollar este sistema.

### La base de datos SQLite esta _zipeada_ ya que su volumen es _grande_.  Debido a eso dentro de la visualizacion de los datso solo se muestran los primeros _40 registros_.

### El sistema posee la habilitacion para el administrador, su **ID** es _user_ y la **contraseña** es _user_.  Dentro del Admin de Django se encuentra la información referente a la base de datos creada en SQLite

![imagen](https://github.com/Carlitos2823/DjangoProject/assets/107945651/de9d93f7-e4f1-4d34-92d4-2d000a32fa89)

![imagen](https://github.com/Carlitos2823/DjangoProject/assets/107945651/79448e9e-4c6d-4b2a-9f33-179413d8b8a9)

### También se tiene acceso al sistema de superusuarios

![imagen](https://github.com/Carlitos2823/DjangoProject/assets/107945651/1bcdf2ea-f0eb-4b80-a690-fe28f56f6654)



