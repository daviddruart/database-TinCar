# database-TinCar
Construcción de una función <p>
Voy a desarrollar una función que calculará el costo del estacionamiento basado en el tiempo de uso. La función tomará la hora de entrada y salida del vehículo, calculará el tiempo total de estacionamiento y luego multiplicará este tiempo por una tarifa horaria.
# Codoigo de la funcion en MySQL
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
