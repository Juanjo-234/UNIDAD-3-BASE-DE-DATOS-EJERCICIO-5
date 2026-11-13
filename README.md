# UNIDAD-3-BASE-DE-DATOS-EJERCICIO-5
El diagrama muestra un **Modelo Relacional (MR)** orientado a la gestión de una institución educativa o universitaria, compuesto por 9 tablas interconectadas que administran las carreras, planes de estudio, asignaturas, comisiones, alumnos, inscripciones y evaluaciones.

A continuación, se detalla la estructura y las relaciones de cada tabla:

---

### 1. Tablas y Estructura

* **CARRERA**
* `CODIGO_CARRERA` (PK)
* `NOMBRE`
* `PLAN_VIGENTE`


* **PLAN_ESTUDIO**
* `ID_PLAN` (PK)
* `NOMBRE`
* `AÑO_VIGENCIA`


* **ASIGNATURAS**
* `CODIGO_ASIGNATURA` (PK)
* `NOMBRE`
* `CARGA_HORARIA`
* `AÑO_CURRICULA`


* **CORRELATIVIDAD** (Tabla autorreferencial / asociativa de materias)
* `CODIGO_ASIGNATURA` (PK / FK)
* `CODIGO_CORRELATIVA` (PK / FK)


* **COMISION**
* `ID_COMISION` (PK)
* `CUPO_MAXIMO`
* `COMISION_LETRA`


* **PROFESOR**
* `MATRICULA` (PK)
* `NOMBRE`
* `ESPECIALIDAD`
* `TELEFONO`


* **ALUMNO**
* `ID_ALUMNO` (PK)
* `NOMBRE`
* `APELLIDO`
* `DNI`
* `CORREO`


* **INSCRIPCION** (Tabla intermedia / asociativa entre Alumno, Comisión y Evaluación)
* `ID_INSCRIPCION` (PK)
* `CONDICION`
* `NOTA_PARCIAL_1`
* `NOTA_PARCIAL_2`


* **EVALUACION**
* `ID_EVALUACION` (PK)
* `FECHA`
* `NOTA`
* `TIPO`



---

### 2. Relaciones Principales

* **Carrera y Plan de Estudio:** Una carrera se organiza a través de uno o varios planes de estudio a lo largo del tiempo (relación de uno a muchos).
* **Plan de Estudio y Asignaturas:** Un plan de estudio contiene múltiples asignaturas que estructuran la currícula académica.
* **Correlatividades:** La tabla `CORRELATIVIDAD` relaciona las asignaturas consigo mismas para definir los requisitos previos (materias correlativas) que un estudiante debe aprobar antes de cursar otra.
* **Asignatura y Comisión:** Una asignatura se dicta en distintas comisiones (divisiones de cursado) para organizar a los alumnos.
* **Comisión y Profesor:** Permite asignar los docentes responsables a cargo del dictado de cada comisión.
* **Alumno e Inscripción:** Un alumno se inscribe en las comisiones de las materias mediante la entidad `INSCRIPCION`, donde se registran las condiciones de cursada y las notas de los parciales.
<img width="1622" height="1161" alt="EJERCICIO 5-MR drawio" src="https://github.com/user-attachments/assets/c3aaad9a-508c-439d-ae78-0e4e8e71c6ef" />


La imagen muestra el proceso completo de **normalización de bases de datos** aplicado de manera secuencial —desde una tabla inicial desnormalizada hasta alcanzar la Tercera Forma Normal (3NF)— para un sistema de gestión académica universitaria (carreras, planes de estudio, asignaturas, correlatividades, ciclos lectivos, comisiones, profesores, alumnos, inscripciones y evaluaciones).

A continuación, se detalla lo que se realiza en cada fase representada en el esquema:

---

### 1. Fase de Normalización N°0 (Tabla Desnormalizada)

* **Estado inicial:** Se parte de una **única tabla grande y plana** que agrupa todos los datos mezclados y redundantes (datos de los alumnos, carreras cursadas, listados completos de asignaturas y correlatividades empaquetados en una sola celda, comisiones, profesores, condiciones y múltiples notas de evaluaciones).
* **Problema:** Presenta anidamientos, grupos repetitivos y redundancia masiva de datos, lo que genera anomalías severas en las operaciones de inserción, actualización y borrado.

### 2. Primera Forma Normal (1NF)

* **Condición:** Se asegura que todos los atributos contengan valores atómicos (indivisibles) y que cada tabla cuente con una clave primaria identificativa.
* **Proceso aplicado:** Se desglosa la información para eliminar los campos multivaluados y estructurar los registros de forma tabular básica:
* **TABLA PLANILLA:** Organiza los datos relacionales iniciales de los alumnos, asignaturas cursadas, comisiones, profesores y notas parciales.
* **TABLA CORRELATIVIDAD:** Se extrae como una tabla independiente para normalizar las relaciones de materias previas requeridas, evitando listas múltiples en una misma celda.



### 3. Segunda Forma Normal (2NF)

* **Condición:** La base de datos debe estar en 1NF y **todos los atributos que no forman parte de la clave deben depender por completo de toda la clave primaria** (eliminando dependencias parciales en tablas con claves compuestas).
* **Proceso aplicado:** Se reestructuran y aíslan las entidades base del sistema educativo:
* **TABLA ALUMNO:** Agrupa los datos personales e institucionales de los estudiantes mediante `ID_ALUMNO` como PK.
* **TABLA ASIGNATURA:** Contiene la información propia de las materias, su carga horaria y el año curricular.
* **TABLA INSCRIPCION y otras tablas operativas:** Estructuran los vínculos funcionales de cursado y calificaciones parciales.



### 4. Tercera Forma Normal (3NF)

* **Condición:** Debe estar en 2NF y **carecer de dependencias transitivas** (ningún atributo no clave debe depender de otro atributo que tampoco sea clave; todo atributo no clave debe depender estrictamente de la clave primaria).
* **Proceso aplicado:** Se estructuran de forma definitiva, modular e independiente todas las entidades del sistema universitario:
* **TABLA CARRERA y PLAN_ESTUDIO:** Aíslan la oferta académica y la vigencia de los planes de estudio.
* **TABLA ASIGNATURA y CORRELATIVIDAD:** Gestionan de manera limpia el catálogo de materias y sus requisitos previos.
* **TABLA CICLO_LECTIVO y COMISION:** Administran la organización temporal de los cursados y sus cupos máximos.
* **TABLA PROFESOR:** Contiene el registro de los docentes y sus especialidades.
* **TABLA ALUMNO:** Mantiene la identidad de los estudiantes de forma independiente.
* **TABLA INSCRIPCION y EVALUACION:** Registran con precisión las condiciones de cursado, las notas parciales, las fechas de exámenes y los tipos de evaluación asociados a cada alumno.
<img width="6580" height="2478" alt="EJERCICIO 5-FASES DE NORMALIZACION drawio" src="https://github.com/user-attachments/assets/187db914-9ab6-45a1-8bc2-9085e5b345b1" />

