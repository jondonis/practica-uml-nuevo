# Diccionario de Clases y Justificaciones de Diseño UML

## 1. CASO 1: Sistema de Gestión Hospitalaria Integral ("HealthFlow")

### Diccionario de Clases
- **Empleado (Abstracta):** Representa a todo el personal del hospital.
   Atributos: # idEmpleado: String, # nombre: String,# salario: double
   Métodos: + calcularSalario(): double
- **Medico:** Especialización de Empleado encargada del seguimiento clínico e intervenciones.
   Atributos: especialidad: Sting ,  exequatur: String
   Métodos: + emitirExpediente(), + realizarIntervencion()
- **Enfermero / Administrativo:** Especializaciones de Empleado con funciones específicas de apoyo y gestión.
- **Paciente:** Persona atendida en el centro médico.
   Atributos: idPaciente: String, nombre: String, fechaNacimiento: Date
- **ExpedienteClinico:** Historial único e insustituible del paciente.
   Atributos: idExpediente: String, fechaCreacion: Date
- **Consulta / Receta:** Registros clínicos individuales asociados al expediente.
- **SalaQuirurgica / EquipoMedico:** Infraestructura y recursos médicos.
- **IntervencionQuirurgica:** Registro transaccional donde interactúan Médicos, Pacientes, Sala e Insumos consumidos.

### Justificación de Relaciones UML
- **Composición entre Paciente y ExpedienteClinico (◆):** El expediente clínico es vitalicio y exclusivo del paciente. No tiene razón de existir sin un paciente asociado.
- **Agregación entre SalaQuirurgica y EquipoMedico (◇):** Los equipos médicos (monitores, bisturíes) pertenecen a la sala pero tienen existencia independiente; un equipo puede ser trasladado a otra sala según requerimiento operativo.


## 2. CASO 2: Plataforma E-Commerce Omnicanal ("GlobalMarket")

### Diccionario de Clases
- **Pedido (Order):** Entidad central de la transacción de compra.
   Atributos: idPedido: String, fecha: Date, estado: String
   Métodos: + calcularTotal(): double
- **DetallePedido (OrderDetail):** Desglose ítem por ítem del pedido.
   Atributos: cantidad: int, precioUnitario: double
- **Item:** Artículo del catálogo con stock disponible.
- **Cliente (Abstracta):** Usuario comprador. Se especializa en ClienteCorporativo (límite de crédito) y ClienteIndividual (fidelización).
- **Pago (Abstracta):** Proceso financiero general. Se especializa mediante herencia en PagoTarjeta, TransferenciaBancaria y Criptomoneda.
- **Envio:** Gestión logística externa generada a partir del pedido.

### Justificación de Relaciones UML
- **Composición entre Pedido y DetallePedido (◆):** Una línea de detalle carece de sentido si el pedido es eliminado. Su ciclo de vida está acoplado fuertemente al pedido.
- **Herencia en Pago:** Permite extender fácilmente nuevos métodos de pago sin alterar la lógica de procesamiento central.



## 3. CASO 3: Gestión Académica y Campus Universitario ("UniCore")

### Diccionario de Clases
- **Facultad:** Unidad académica principal de la universidad.
- **Carrera:** Programa académico dictado por una facultad.
- **Pensum:** Plan de estudios oficial estructurado por asignaturas.
- **Asignatura:** Materia académica que posee créditos (UV) y prerrequisitos.
- **RegistroMatricula / GrupoClase / Docente / Aula:** Entidades encargadas de la gestión operativa de inscripción y asignación física.

### Justificación de Relaciones UML
- **Composición entre Facultad y Carrera (◆):** Especificación estricta del negocio: si una facultad cierra, las carreras pertenecientes a ella se dan de baja automáticamente.
- **Asociación Reflexiva en Asignatura:** Modela los prerrequisitos académicos, donde una asignatura apunta a otras asignaturas previas requeridas.
- **Agregación entre Aula y GrupoClase (◇):** Las aulas son parte de la infraestructura del campus y existen independientemente de si se imparten clases en ellas en un ciclo determinado.
