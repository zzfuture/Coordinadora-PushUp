# COORDINADORA PUSHUP

Realtional database for the management of a shipping company

**SQL**

```sql
CREATE TABLE `usuario` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `username` varchar(50) UNIQUE NOT NULL,
  `password` varchar(150) UNIQUE NOT NULL,
  `email` varchar(100) UNIQUE NOT NULL
);

CREATE TABLE `rol` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50) UNIQUE NOT NULL
);

CREATE TABLE `userrol` (
  `idUsuarioFk` int NOT NULL,
  `idRolFk` int NOT NULL,
  PRIMARY KEY (`idUsuarioFk`, `idRolFk`)
);

CREATE TABLE `empleado` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50),
  `apellido` varchar(50),
  `email` varchar(50),
  `idOficinaFk` int,
  `idPuestoFk` int
);

CREATE TABLE `puesto` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50)
);

CREATE TABLE `pais` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50) UNIQUE
);

CREATE TABLE `departamento` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50) UNIQUE,
  `idPaisFk` int NOT NULL
);

CREATE TABLE `ciudad` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50) UNIQUE,
  `idDepartamentoFk` int NOT NULL
);

CREATE TABLE `direccion` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `tipo_via` varchar(50),
  `numero_principal` smallint,
  `letra_principal` char(2),
  `bis` char(10),
  `letra_secundaria` char(2),
  `cardinal_primario` char(10),
  `numero_secundario` smallint,
  `cardinal_secundario` char(10),
  `complemento` varchar(50),
  `idCiudadFk` int
);

CREATE TABLE `oficina` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `telefono` int,
  `idDireccionFk` int NOT NULL
);

CREATE TABLE `paquete` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `idDetallePaqueteFk` int NOT NULL,
  `idTipoPaqueteFk` int NOT NULL,
  `idEnvioFk` int NOT NULL
);

CREATE TABLE `detalle_paquete` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `largo` float(3),
  `ancho` float(3),
  `alto` float(3),
  `peso` float(3)
);

CREATE TABLE `tipo_paquete` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50)
);

CREATE TABLE `envio` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `idTipoEnvio` int,
  `idEstadoEnvioFk` int,
  `idRutaEnvioFk` int,
  `idUbicacionFk` int,
  `idDetalleEnvioFk` int
);

CREATE TABLE `detalle_envio` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `fechaSalida` date,
  `fechaEstimada` date,
  `fechaEntrega` date,
  `cantidad` int,
  `idPagoFk` int
);

CREATE TABLE `tipo_envio` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50)
);

CREATE TABLE `estado_envio` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50)
);

CREATE TABLE `ruta_envio` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `idOficinaFk` int,
  `idClienteFk` int
);

CREATE TABLE `ubicacion_envio` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `localizacion` varchar(50),
  `descripcion` varchar(200)
);

CREATE TABLE `cliente` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `cedula` int,
  `nombre` varchar(50),
  `apellido` varchar(50),
  `email` varchar(50),
  `telefono` int,
  `idDireccionFk` int
);

CREATE TABLE `pago` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `total` int,
  `fechaPago` date,
  `idClienteFk` int,
  `idFormaPagoFk` int
);

CREATE TABLE `forma_pago` (
  `id` int UNIQUE PRIMARY KEY NOT NULL AUTO_INCREMENT,
  `nombre` varchar(50)
);

ALTER TABLE `usuario` ADD FOREIGN KEY (`id`) REFERENCES `userrol` (`idUsuarioFk`);

ALTER TABLE `rol` ADD FOREIGN KEY (`id`) REFERENCES `userrol` (`idRolFk`);

ALTER TABLE `pais` ADD FOREIGN KEY (`id`) REFERENCES `departamento` (`idPaisFk`);

ALTER TABLE `departamento` ADD FOREIGN KEY (`id`) REFERENCES `ciudad` (`idDepartamentoFk`);

ALTER TABLE `ciudad` ADD FOREIGN KEY (`id`) REFERENCES `direccion` (`idCiudadFk`);

ALTER TABLE `direccion` ADD FOREIGN KEY (`id`) REFERENCES `oficina` (`idDireccionFk`);

ALTER TABLE `oficina` ADD FOREIGN KEY (`id`) REFERENCES `empleado` (`idOficinaFk`);

ALTER TABLE `puesto` ADD FOREIGN KEY (`id`) REFERENCES `empleado` (`idPuestoFk`);

ALTER TABLE `detalle_paquete` ADD FOREIGN KEY (`id`) REFERENCES `paquete` (`idDetallePaqueteFk`);

ALTER TABLE `tipo_paquete` ADD FOREIGN KEY (`id`) REFERENCES `paquete` (`idTipoPaqueteFk`);

ALTER TABLE `envio` ADD FOREIGN KEY (`id`) REFERENCES `paquete` (`idEnvioFk`);

ALTER TABLE `pago` ADD FOREIGN KEY (`id`) REFERENCES `detalle_envio` (`idPagoFk`);

ALTER TABLE `tipo_envio` ADD FOREIGN KEY (`id`) REFERENCES `envio` (`idTipoEnvio`);

ALTER TABLE `ruta_envio` ADD FOREIGN KEY (`id`) REFERENCES `envio` (`idRutaEnvioFk`);

ALTER TABLE `ubicacion_envio` ADD FOREIGN KEY (`id`) REFERENCES `envio` (`idUbicacionFk`);

ALTER TABLE `estado_envio` ADD FOREIGN KEY (`id`) REFERENCES `envio` (`idEstadoEnvioFk`);

ALTER TABLE `detalle_envio` ADD FOREIGN KEY (`id`) REFERENCES `envio` (`idDetalleEnvioFk`);

ALTER TABLE `oficina` ADD FOREIGN KEY (`id`) REFERENCES `ruta_envio` (`idOficinaFk`);

ALTER TABLE `cliente` ADD FOREIGN KEY (`id`) REFERENCES `ruta_envio` (`idClienteFk`);

ALTER TABLE `cliente` ADD FOREIGN KEY (`id`) REFERENCES `pago` (`idClienteFk`);

ALTER TABLE `forma_pago` ADD FOREIGN KEY (`id`) REFERENCES `pago` (`idFormaPagoFk`);

ALTER TABLE `direccion` ADD FOREIGN KEY (`id`) REFERENCES `cliente` (`idDireccionFk`);

```


