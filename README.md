# DjangoProject
Proyecto de Python con Framework Django y base de datos SQLite

EL sistema muesra el archivo CSV sacado de la fuente de internet https://www.stats.govt.nz/large-datasets/csv-files-for-download/

Ademas a continuacion se comparte el codigo para pasar desde el dataset CSV a una base de datos llamada libreria diseñada en SQLite

**** CODIGO PARA PASAR DE UN CSV A UNA TABLA DE SQLITE ****
import csv
import sqlite3

# Nombre del archivo CSV y nombre de la tabla SQLite
csv_filename = 'data.csv'
sqlite_db_filename = 'libreria.db'

# Conectarse a la base de datos SQLite
conn = sqlite3.connect(sqlite_db_filename)
cursor = conn.cursor()

# Abrir el archivo CSV y leer los datos
with open(csv_filename, 'r') as csv_file:
    csv_reader = csv.reader(csv_file)
    next(csv_reader)  # Para omitir la fila de encabezados si la tienes en el archivo CSV
    for row in csv_reader:
        # Insertar los datos en la tabla SQLite
        cursor.execute('''
            INSERT INTO libreria_dato ( Direction , Year, Date, Weekday, Country, Commodity, Transport_Mode, Measure, Value, Cumulative)
            VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
        ''', (row[0], row[1], row[2], row[3], row[4], row[5], row[6], row[7], row[8], row[9] ))  # Ajusta los índices según la estructura de tu CSV

# Guardar los cambios y cerrar la conexión a la base de datos
conn.commit()
conn.close()
