# Complemento Técnico – TFM Carla Pesántez

## Tema del TFM

**Evaluación Comparativa de Soluciones Cyber Range en Nube Pública y Arquitecturas Híbridas, con Desarrollo de un Complemento Comunitario para OpenNebula**

Este repositorio contiene el complemento técnico desarrollado para el Trabajo Final de Maestría en Ciberseguridad y Privacidad – Seguridad en el Cloud.
El trabajo se enfoca en la validación de un entorno local basado en OpenNebula MiniONE sobre Ubuntu 22.04 LTS, ejecutado en VirtualBox con configuración NAT + Port Forwarding.

El diseño del complemento está inspirado en la lógica modular de KYPO Cyber Range, adaptado a un sandbox local para pruebas controladas y reproducibles.



----------
## Estructura del repositorio

- **Copia_de_TFMlocal.ipynb** – Notebook principal desarrollado en Google Colab.  
Este notebook contiene el mismo código que el archivo `TFMlocal.py` utilizado en Ubuntu durante la validación en MiniONE.

- **TFMlocal.py** – Versión del complemento ejecutada en Ubuntu dentro del entorno real (MiniONE + VirtualBox).  
Este archivo corresponde a la ejecución en modo simulación y pruebas de interacci{on con la API.

- **logs/** – Carpeta de logs generados durante la validación (almacenados en Google Drive).

- **README.md** – Documentación del repositorio.

## Correspondencia entre archivos

- **TFMlocal.py** → Archivo ejecutado en Ubuntu dentro del entorno real (MiniONE).  
- **Copia_de_TFMlocal.ipynb** → Notebook equivalente usado en Google Colab para validación en modo simulación.

Ambos contienen la misma lógica del complemento, adaptada al entorno de ejecución.

--------------
##  Alcance y capacidades del complemento ##

El complemento fue diseñado para operar en entornos OpenNebula reales, donde es posible gestionar escenarios multiusuario.
Las funciones desarrolladas permiten que distintos estudiantes, grupos o instituciones puedan aprovisionar laboratorios de manera independiente utilizando:

* plantillas diferenciadas

* roles

* permisos

* flujos de despliegue aislados

Aunque la validación práctica se realizó en un entorno local monousuario (MiniONE), el diseño del complemento es compatible con despliegues OpenNebula más robustos que sí soportan:

* multiusuario

* multi-tenant

* control de permisos granular

Esto permite que el complemento pueda integrarse en entornos educativos reales donde varios usuarios trabajan simultáneamente sin interferir entre sí.
------------------

## Requisitos del entorno: 

El desarrollo, ejecución y validación del complemento se realizaron utilizando el siguiente entorno técnico:

- **Lenguaje:** Python 3.x  
- **Entorno de desarrollo distribuido:** Google Colab (pruebas conceptuales, revisión modular y control de versiones)  
- **Plataforma de orquestación:** OpenNebula 6.x desplegado mediante MiniONE  
- **Sistema operativo base:** Ubuntu 22.04 LTS  
- **Virtualización local:** VirtualBox sobre host Windows 11 (modo NAT + Port Forwarding)  
- **Acceso remoto y transferencia:** SSH y WinSCP  
- **Interfaz de gestión:** FireEdge / Sunstone  
- **Repositorio de código:** GitHub  
- **Plantillas utilizadas:** Alpine Linux 3.2  
- **Herramientas previstas (no utilizadas en la validación final):** Nmap, Wireshark y DVWA  

Aunque inicialmente se planificó utilizar Google Colab como entorno principal de desarrollo distribuido, su uso se centró en la validación conceptual del diseño y en la ejecución en modo simulación. Su integración con GitHub facilitó la trazabilidad y el control de versiones durante el desarrollo.


<img width="864" height="649" alt="image" src="https://github.com/user-attachments/assets/ec756005-703e-4ea9-843c-6bf8c0bb2778" />

Figura 1: Arquitectura del entorno técnico. Fuente: Elaboración propia en Canva.

--------------

##  Objetivo del complemento técnico

El complemento implementa un flujo modular que permite:

- Configurar un entorno local MiniONE
- Autenticarse contra la API XML-RPC de OpenNebula 
- Instanciar máquinas virtuales desde plantillas 
- Simular configuración de red 
- Registrar eventos para trazabilidad y auditoría 
- Ejecutar un flujo principal tipo laboratorio CTF 

Este código fue utilizado como parte del proceso de validación técnica del TFM.



----------------------------
##  Arquitectura del complemento

El complemento técnico desarrollado para el TFM está organizado en módulos funcionales que permiten una ejecución clara, trazable y adaptable. Cada módulo cumple una función específica dentro del flujo tipo CTF, desde la configuración inicial hasta la generación de logs.

La arquitectura modular facilita la comprensión del código, su mantenimiento y su posible extensión hacia entornos más complejos. El diseño está inspirado en la lógica de KYPO Cyber Range, adaptado a un entorno local reproducible.

La siguiente figura muestra la estructura conceptual del script `tfmlocal.py`, implementado en Google Colab y validado en modo simulación:

<img width="1061" height="760" alt="image" src="https://github.com/user-attachments/assets/1178788d-de65-4d36-9ba3-06babab16c2b" />


*Figura 2: Estructura modular del complemento implementado en Google Colab. Fuente: Elaboración propia en Canva.*


El código está organizado en módulos:

1. **Configuración del entorno**  
2. **Autenticación XML-RPC**  
3. **Despliegue de máquinas virtuales**  
4. **Simulación de red**  
5. **Registro de eventos**  
6. **Flujo principal del complemento**  

El diseño permite añadir futuros entornos (por ejemplo, nube pública) sin modificar la lógica interna.


##  Modo Simulación

El complemento incluye un modo de simulación controlado por la variable:

MODO_SIMULACION = True  # Simulación

MODO_SIMULACION = False  # Modo real

- **MODO_SIMULACION = True**  
  - No ejecuta llamadas reales a OpenNebula  
  - Imprime acciones  
  - Registra eventos  
  - Ideal para pruebas conceptuales

- **MODO_SIMULACION = False**  
  - Ejecuta llamadas reales a la API XML-RPC  
  - Requiere credenciales válidas de `oneadmin`

---------

## Ejecución del complemento

### 1. Ejecución desde el notebook (Google Colab o Jupyter)

**Pasos de ejecución:**

1. Abrir **Copia_de_TFMlocal.ipynb**.
2. Activar o desactivar el modo simulación modificando la variable: **MODO_SIMULACION**

  MODO_SIMULACION = True   # Simulación
  MODO_SIMULACION = False  # Modo real

3. Si se usa modo real, ajustar las credenciales de **oneadmin**.

4. Ejecutar todas las celdas hasta llegar al flujo principal.

5. Ejecutar:
     **ejecutar_complemento()**
   ------------------------

### 2. Ejecucion desde Ubuntu (archivo TFMlocal.py)
En el entorno Ubuntu + MiniONE, el complemento se ejecuta por defecto en modo simulación, ya que:
**MODO_SIMULACION = True**
Este modo permite validar la lógica, rutas, permisos y generación de logs dentro del entorno real sin depender de la estabilidad de la API XML-RPC.

**Pasos de ejecucion**

  1. Abrir una terminal en la carpeta del archivo **TFMlocal.py.**
  2. Ejecutar el complemento directamente (no es necesario modificar nada para modo simulación):
  **python3 TFMlocal.py**
  3. Revisar los logs generados en la carpeta **logs/** dentro del propio entorno local (sandbox).

**NOTA:**

El modo real (**MODO_SIMULACION = False**) no se utilizó en MiniONE debido a:

- inestabilidad de la API XML-RPC

- reinicios del servicio

- latencia

- fallos de conexión

- limitaciones del entorno VirtualBox NAT

El modo real queda disponible para entornos OpenNebula más robustos.

-----

## Validación del complemento

La validación del complemento se realizó en dos entornos:
  1) **Google Colab** (entorno no real, sin acceso a la API XML-RPC)
  2) **Ubuntu + MiniONE** (entorno real, sandbox local)

Este enfoque permitió comprobar la lógica del complemento, su trazabilidad y su funcionamiento dentro de un entorno OpenNebula operativo, sin depender de infraestructura compleja.

## 1. Validación en Google Colab (modo simulación)

Google Colab no permite comunicación con redes locales ni con puertos personalizados, por lo que no es posible acceder a la API XML-RPC de OpenNebula.
Por esta razón, la validación se realizó exclusivamente en modo simulación.

En este modo, el sistema:

- Ejecuta el flujo principal

- Registra acciones en consola

- Genera logs con timestamps

- Valida la lógica modular sin llamar a la API
  
--------------------
## 2. Validación en Ubuntu + MiniONE (entorno real)
El complemento también fue ejecutado en un entorno real basado en:

- Ubuntu 22.04

- MiniONE (OpenNebula)

- VirtualBox

Se validó:

- Rutas y permisos

- Estructura de carpetas

- Generación de logs reales

- Funcionamiento del script en un entorno OpenNebula operativo


## 3. Validación manual de roles

Se verificó manualmente desde la interfaz de MiniONE que:

- Las VMs se crean correctamente

- Pueden iniciarse desde la interfaz

- Operan como se espera en un escenario educativo tipo CTF (Capture the Flag)


## Conclusión de la validación

La combinación de validación en Colab, validación en entorno real y verificación manual demuestra que el complemento es:

- Funcional

- Reproducible

- Portable

Adecuado para entornos educativos con recursos limitados

--------------------------------------------------------
## LIMITACIONES DEL ENTORNO Y LA VALIDACIÓN

Durante el desarrollo y validación se identificaron varias limitaciones:

- **Sin acceso al laboratorio cloud institucional (AWS/UOC)** 
→ Obligó a trabajar en un entorno local reducido.

-**Imposibilidad de utilizar la API XML-RPC en la validación práctica** 
→ MiniONE es monousuario e inestable para llamadas reales.
→ Colab no puede comunicarse con redes locales ni puertos personalizados.
→ La validación se realizó íntegramente en modo simulación.

- **Dependencia de VirtualBox en modo NAT con port forwarding**  
→ Limita la exposición de servicios y afecta la conectividad.
→ Impide pruebas reales estables con la API XML-RPC.

-**Escenario monousuario en MiniONE**  
→ No fue posible validar la lógica multiusuario del complemento.

-**Ausencia de pruebas con herramientas avanzadas (Nmap, Wireshark, DVWA)** 
→ Se consideraron conceptualmente, pero no se ejecutaron por restricciones del entorno.

Estas limitaciones no afectan la validez conceptual del complemento, sino que señalan áreas de mejora para futuras implementaciones en entornos OpenNebula más robustos.

----------
## Proyección y limitaciones del entorno

El complemento fue validado en un entorno monousuario basado en MiniONE; sin embargo, su diseño sigue criterios de interoperabilidad y potencial comunitario. Esto permite su futura adaptación a:

* programas de formación con múltiples estudiantes,

* laboratorios compartidos entre facultades o centros,

* iniciativas interuniversitarias,

* infraestructuras federadas en nube pública e híbrida.

La validación confirma que el complemento funciona correctamente en un entorno reducido, mientras que su arquitectura modular garantiza la posibilidad de extenderlo a ecosistemas multiusuario y distribuidos, coherentes con el objetivo formativo del proyecto.

Las pruebas avanzadas tipo CTF no pudieron realizarse debido a las limitaciones inherentes de MiniONE y del hardware disponible. MiniONE está diseñado para uso monousuario y para un número reducido de máquinas virtuales, lo que impide desplegar topologías complejas, múltiples roles simultáneos o servicios vulnerables necesarios para un CTF real. La imposibilidad de habilitar redes en modo Bridge y las restricciones de memoria y CPU del equipo anfitrión limitaron la creación de escenarios aislados con tráfico controlado.

Por razones éticas y de seguridad, tampoco se habilitaron vulnerabilidades reales fuera de un entorno completamente aislado. En conjunto, estos factores justifican que la validación se centrara en pruebas básicas de aprovisionamiento y simulación, tal como se definió en la metodología.
