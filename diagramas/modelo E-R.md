# Modelo Entidad-Relación - Comemos Seguros

## Entidades principales

1. **Usuario**
   - Atributos: `UsuarioID` (PK), `Nombre`, `Email`, `Telefono`, `TipoUsuario` (administrativo, cocina, gestión), `Permisos`, `CentroID` (FK)

2. **Centro**
   - Atributos: `CentroID` (PK), `Nombre`, `Direccion`, `TipoCentro` (educativo, sanitario, otro), `Telefono`

3. **Producto**
   - Atributos: `ProductoID` (PK), `Nombre`, `Marca`, `Categoria`, `Calorias`, `Descripcion`

4. **Ingrediente**
   - Atributos: `IngredienteID` (PK), `Nombre`, `Descripcion`

5. **Alergeno**
   - Atributos: `AlergenoID` (PK), `Nombre`, `Descripcion`

6. **Menu**
   - Atributos: `MenuID` (PK), `Nombre`, `Fecha`, `Periodo` (diario, semanal), `TipoMenu` (almuerzo, cena, mixto), `CentroID` (FK), `UsuarioID` (FK)

7. **Plato**
   - Atributos: `PlatoID` (PK), `Nombre`, `Descripcion`, `Calorias`, `MenuID` (FK)

8. **Alerta**
   - Atributos: `AlertaID` (PK), `FechaHora`, `NivelRiesgo`, `Mensaje`, `UsuarioID` (FK), `MenuID` (FK), `ProductoID` (FK)

9. **HistorialMenu**
   - Atributos: `HistorialMenuID` (PK), `MenuID` (FK), `FechaModificacion`, `Accion` (creado, editado, validado), `UsuarioID` (FK), `Detalle`

## Relaciones y cardinalidades

- **Centro - Usuario**: un centro puede tener muchos usuarios. Cada usuario pertenece a un solo centro.
  - Cardinalidad: Centro 1 -- N Usuario

- **Centro - Menu**: un centro puede tener muchos menús. Cada menú pertenece a un solo centro.
  - Cardinalidad: Centro 1 -- N Menu

- **Usuario - Menu**: un usuario puede crear o validar muchos menús. Un menú es gestionado por un solo usuario principal.
  - Cardinalidad: Usuario 1 -- N Menu

- **Menu - Plato**: un menú puede contener muchos platos. Un plato pertenece a un solo menú.
  - Cardinalidad: Menu 1 -- N Plato

- **Plato - Ingrediente**: un plato puede tener muchos ingredientes y un ingrediente puede formar parte de muchos platos.
  - Relación intermedia: `PlatoIngrediente`
  - Cardinalidad: Plato N -- M Ingrediente

- **Producto - Ingrediente**: un producto puede contener muchos ingredientes y un ingrediente puede estar en muchos productos.
  - Relación intermedia: `ProductoIngrediente`
  - Cardinalidad: Producto N -- M Ingrediente

- **Producto - Alergeno**: un producto puede presentar varios alérgenos y un alérgeno puede estar presente en muchos productos.
  - Relación intermedia: `ProductoAlergeno`
  - Cardinalidad: Producto N -- M Alergeno

- **Usuario - Alergeno**: un usuario puede tener varias alergias y un alérgeno puede afectar a muchos usuarios.
  - Relación intermedia: `UsuarioAlergeno`
  - Cardinalidad: Usuario N -- M Alergeno

- **Menu - Alerta**: un menú puede generar muchas alertas de conflicto. Cada alerta se asocia a un solo menú.
  - Cardinalidad: Menu 1 -- N Alerta

- **Producto - Alerta**: un producto puede ser motivo de muchas alertas.
  - Cardinalidad: Producto 1 -- N Alerta

- **Usuario - HistorialMenu**: un usuario puede generar mucho historial. Cada registro de historial se asocia a un solo usuario.
  - Cardinalidad: Usuario 1 -- N HistorialMenu

- **Menu - HistorialMenu**: un menú puede tener muchas modificaciones registradas. Cada historial pertenece a un solo menú.
  - Cardinalidad: Menu 1 -- N HistorialMenu

## Tablas asociativas

- **PlatoIngrediente**
  - Atributos: `PlatoIngredienteID` (PK), `PlatoID` (FK), `IngredienteID` (FK), `Cantidad`, `Unidad`

- **ProductoIngrediente**
  - Atributos: `ProductoIngredienteID` (PK), `ProductoID` (FK), `IngredienteID` (FK), `Porcentaje`

- **ProductoAlergeno**
  - Atributos: `ProductoAlergenoID` (PK), `ProductoID` (FK), `AlergenoID` (FK)

- **UsuarioAlergeno**
  - Atributos: `UsuarioAlergenoID` (PK), `UsuarioID` (FK), `AlergenoID` (FK), `GradoSensibilidad`

## Explicación breve

Este modelo E-R representa un sistema de gestión de menús y control de alérgenos para centros colectivos. Los usuarios, organizados por centros y roles, gestionan menús asociados a fechas y restricciones alimentarias. Los productos se descomponen en ingredientes y alérgenos, lo que permite detectar conflictos antes de validar la oferta y generar alertas.

El historial de menús asegura trazabilidad de cambios, incidencias y ajustes a lo largo del tiempo, lo que mejora la seguridad alimentaria y facilita la revisión posterior.
