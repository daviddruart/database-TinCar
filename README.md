# Construcción de una función <p>
Voy a desarrollar una función que calculará el costo del estacionamiento basado en el tiempo de uso. La función tomará la hora de entrada y salida del vehículo, calculará el tiempo total de estacionamiento y luego multiplicará este tiempo por una tarifa horaria.
# Codigo de la funcion en MySQL
    DELIMITER //
    
    CREATE FUNCTION calcular_costo_estacionamiento(
        hora_entrada DATETIME,
        hora_salida DATETIME,
        tarifa_hora DECIMAL(10, 2)
    )
    RETURNS DECIMAL(10, 2)
    DETERMINISTIC
    BEGIN
        DECLARE tiempo_total DECIMAL(10, 2);
        DECLARE costo_total DECIMAL(10, 2);
    
        -- Calcular el tiempo total en horas
        SET tiempo_total = TIMESTAMPDIFF(MINUTE, hora_entrada, hora_salida) / 60.0;
    
        -- Calcular el costo total
        SET costo_total = tiempo_total * tarifa_hora;
    
        RETURN costo_total;
    END //
    
    DELIMITER ;
# Explicación de la Función
Parámetros de Entrada:

    hora_entrada: 
La fecha y hora en que el vehículo ingresó al parqueadero.

    hora_salida: 
La fecha y hora en que el vehículo salió del parqueadero.

    tarifa_hora: 
La tarifa que se cobra por cada hora de estacionamiento.

# Proceso:

La función primero calcula el tiempo_total que el vehículo estuvo estacionado en horas, utilizando la función TIMESTAMPDIFF, que calcula la diferencia entre dos fechas en minutos y luego se divide entre 60 para convertirlo a horas.
Luego, multiplica el tiempo_total por la tarifa_hora para obtener el costo_total.

# Uso de la Función
Con esta función se ve el calculo del costo en el estacionamiento de un vehículo específico:

    SELECT calcular_costo_estacionamiento('2024-09-03 08:00:00', '2024-09-03 10:30:00', 2.50) AS costo;
Esto calculará el costo para un vehículo que estuvo estacionado desde las 08:00 hasta las 10:30, con una tarifa de $2.50 por hora.

# Tabla relacionada
    CREATE TABLE registro_vehiculos (
        id INT AUTO_INCREMENT PRIMARY KEY,
        placa VARCHAR(10) NOT NULL,
        hora_entrada DATETIME NOT NULL,
        hora_salida DATETIME,
        tarifa_hora DECIMAL(10, 2) NOT NULL
    );
# Datos ingresados
    INSERT INTO registro_vehiculos (placa, hora_entrada, hora_salida, tarifa_hora)
    VALUES
    ('ABC123', '2024-09-03 08:00:00', '2024-09-03 10:30:00', 2.50),
    ('XYZ789', '2024-09-03 09:15:00', '2024-09-03 11:45:00', 3.00),
    ('LMN456', '2024-09-03 07:45:00', '2024-09-03 09:00:00', 1.75)
    ;
    
