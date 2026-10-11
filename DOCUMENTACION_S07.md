# Documentación del Proyecto: Sistema de Gestión Veterinaria

## 1. Estructura del diseño detallado de la historia de usuario
Para estandarizar el recojo de información y el desarrollo del sistema, se utilizará la siguiente plantilla para el diseño detallado de las Historias de Usuario (HU)[cite: 3]:

| Campo | Descripción |
| :--- | :--- |
| **ID y Título** | Identificador único (ej. HU-01) y un título descriptivo breve. |
| **Rol (Actor)** | Quién interactúa con el sistema (Recepcionista, Veterinario, Admin). |
| **Descripción** | Formato estándar: *Como [Rol], quiero [Acción] para [Beneficio/Razón].* |
| **Precondiciones** | Qué debe cumplirse antes de ejecutar la acción (ej. Estar logueado). |
| **Criterios de Aceptación** | Condiciones que determinan si la historia está terminada. Formato BDD: *Dado que [Contexto], Cuando [Acción], Entonces [Resultado esperado].* |

---

## 2. Historias de usuario reales (Recojo de información)
A partir del análisis de las necesidades de la clínica veterinaria, se han levantado las siguientes historias de usuario principales[cite: 3]:

### HU-01: Gestión de Citas
* **Rol:** Recepcionista
* **Descripción:** Como recepcionista, quiero agendar, reprogramar o cancelar citas veterinarias para mantener un orden en la atención diaria.
* **Precondiciones:** El cliente y la mascota deben estar registrados en el sistema.
* **Criterios de Aceptación:** 
  * *Dado que* un cliente solicita una cita, *Cuando* ingreso la fecha y hora seleccionada, *Entonces* el sistema valida que no haya cruce de horarios con otro paciente y guarda la cita en estado "Pendiente".

### HU-02: Registro de Historial Clínico
* **Rol:** Veterinario
* **Descripción:** Como veterinario, quiero registrar el diagnóstico, tratamiento y observaciones de cada consulta para llevar un seguimiento de la salud de la mascota.
* **Precondiciones:** La cita debe estar en estado "En atención".
* **Criterios de Aceptación:**
  * *Dado que* finalizo la revisión médica, *Cuando* guardo los datos del diagnóstico y la receta, *Entonces* el sistema añade un nuevo registro inmutable al historial de la mascota con la fecha actual.

### HU-03: Control de Stock y Ventas
* **Rol:** Administrador / Recepcionista
* **Descripción:** Como administrador, quiero que el inventario se actualice automáticamente tras una venta para evitar quiebres de stock.
* **Precondiciones:** El producto debe existir en la base de datos con stock > 0.
* **Criterios de Aceptación:**
  * *Dado que* registro el pago de un desparasitante, *Cuando* confirmo la venta, *Entonces* el sistema resta la cantidad vendida del inventario y lanza una alerta visual si el stock llega al límite mínimo.

---

## 3. Requerimientos Funcionales (40 documentados)
A continuación, se listan los requerimientos funcionales del sistema, divididos por módulos, cumpliendo con la exigencia de documentar al menos 40 ítems[cite: 3]:

**Módulo de Seguridad y Autenticación**
1. **RF-01:** El sistema debe permitir el inicio de sesión mediante usuario y contraseña.
2. **RF-02:** El sistema debe validar las credenciales contra la base de datos SQLite.
3. **RF-03:** El sistema debe bloquear temporalmente al usuario tras 3 intentos fallidos de acceso.
4. **RF-04:** El sistema debe permitir al usuario cerrar su sesión de forma segura.
5. **RF-05:** El sistema debe restringir el acceso a módulos según el rol (Admin, Vet, Recepcionista).

**Módulo de Clientes**
6. **RF-06:** El sistema debe permitir registrar un nuevo cliente con datos obligatorios (DNI/RUC, Nombres, Teléfono).
7. **RF-07:** El sistema debe validar que el DNI no se encuentre duplicado al registrar.
8. **RF-08:** El sistema debe permitir editar la información de contacto de un cliente existente.
9. **RF-09:** El sistema debe permitir buscar clientes por nombre o DNI.
10. **RF-10:** El sistema debe realizar un borrado lógico (deshabilitar) en lugar de eliminar clientes para mantener integridad.

**Módulo de Mascotas**
11. **RF-11:** El sistema debe permitir registrar una mascota asignándola a un cliente existente.
12. **RF-12:** El sistema debe almacenar especie, raza, peso, edad y sexo de la mascota.
13. **RF-13:** El sistema debe permitir modificar los datos físicos de la mascota.
14. **RF-14:** El sistema debe permitir buscar mascotas por su nombre o ID.
15. **RF-15:** El sistema debe mostrar una lista filtrada de las mascotas pertenecientes a un cliente específico.

**Módulo de Gestión de Citas**
16. **RF-16:** El sistema debe permitir agendar una cita vinculada a un cliente, una mascota y un veterinario.
17. **RF-17:** El sistema debe permitir reprogramar la fecha y hora de una cita pendiente.
18. **RF-18:** El sistema debe permitir cambiar el estado de la cita (Pendiente, Atendida, Cancelada).
19. **RF-19:** El sistema debe mostrar una alerta si se intenta agendar en un horario ya ocupado por el mismo veterinario.
20. **RF-20:** El sistema debe proveer una vista del listado de citas programadas para el día actual.
21. **RF-21:** El sistema debe permitir filtrar el listado de citas por veterinario asignado.
22. **RF-22:** El sistema debe calcular automáticamente la duración estimada de la cita (por defecto 30 minutos).

**Módulo de Historial Clínico**
23. **RF-23:** El sistema debe permitir abrir un nuevo formulario de consulta desde una cita programada.
24. **RF-24:** El sistema debe permitir registrar los síntomas ingresados y el peso actual en la consulta.
25. **RF-25:** El sistema debe permitir ingresar el diagnóstico emitido por el veterinario.
26. **RF-26:** El sistema debe permitir registrar los medicamentos recetados y el tratamiento a seguir.
27. **RF-27:** El sistema debe permitir visualizar cronológicamente el historial clínico de una mascota.
28. **RF-28:** El sistema debe permitir exportar el detalle de una consulta clínica específica (receta).
29. **RF-29:** El sistema debe bloquear la edición de un historial clínico pasado (inmutabilidad legal).

**Módulo de Inventario (Productos/Medicamentos)**
30. **RF-30:** El sistema debe permitir registrar un nuevo producto con código, nombre, categoría, precio y stock inicial.
31. **RF-31:** El sistema debe permitir actualizar el precio y la descripción de un producto.
32. **RF-32:** El sistema debe descontar existencias automáticamente al realizarse una venta.
33. **RF-33:** El sistema debe permitir el ajuste manual de inventario (ingresos por nuevas compras).
34. **RF-34:** El sistema debe notificar en pantalla los productos que tengan un stock igual o menor a 5 unidades.
35. **RF-35:** El sistema debe permitir buscar productos en el inventario por código o palabras clave.

**Módulo de Ventas y Facturación Interna**
36. **RF-36:** El sistema debe permitir generar un ticket de venta agregando múltiples productos o servicios.
37. **RF-37:** El sistema debe calcular el subtotal y el total a pagar automáticamente.
38. **RF-38:** El sistema debe registrar el método de pago utilizado (Efectivo, Yape, Plin).

**Módulo de Reportes**
39. **RF-39:** El sistema debe generar un reporte tabular de las citas atendidas en un rango de fechas.
40. **RF-40:** El sistema debe generar un reporte de las ventas consolidadas del día.
41. **RF-41:** El sistema debe generar un listado de los 10 productos más vendidos del mes.

---

## 4. Requerimientos No Funcionales
Para garantizar la viabilidad técnica y usabilidad del proyecto en el curso, se establecen los siguientes RNF[cite: 3]:

* **RNF-01 (Arquitectura y Persistencia):** El sistema debe estar desarrollado aplicando el patrón MVC y Programación Orientada a Objetos, utilizando SQLite como base de datos local embebida.
* **RNF-02 (Usabilidad):** Las interfaces gráficas (vistas) deben ser intuitivas, permitiendo acceder a los procesos principales (como agendar cita o realizar venta) en un máximo de 3 clics.
* **RNF-03 (Rendimiento):** El tiempo de respuesta para consultas a la base de datos (ej. buscar un historial clínico) no debe exceder los 2 segundos.
* **RNF-04 (Compatibilidad):** El aplicativo de escritorio debe ser funcional y ejecutable en sistemas operativos Windows 10 y Windows 11 sin necesidad de servidores externos.
* **RNF-05 (Seguridad):** Las contraseñas de los usuarios deben estar encriptadas/hasheadas en la base de datos y no guardarse en texto plano.