# Complemento Técnico – TFM Carla Pesántez

## Tema del TFM

**Evaluación Comparativa de Soluciones Cyber Range en Nube Pública y Arquitecturas Híbridas, con Desarrollo de un Complemento Comunitario para OpenNebula**

Este repositorio contiene el complemento técnico desarrollado para el Trabajo Final de Maestria en Ciberseguridad y Privacidad- Seguridad en el Cloud, enfocado en la validación de un entorno local basado en OpenNebula MiniONE sobre Ubuntu 22.04 LTS, ejecutado en VirtualBox con configuración NAT + Port Forwarding.

El diseño está inspirado en la lógica modular de KYPO Cyber Range, adaptado a un sandbox local para pruebas controladas y reproducibles.
--------------
##  Alcance y capacidades del complemento ##

- El complemento fue diseñado para operar en entornos OpenNebula reales, donde es posible gestionar escenarios multiusuario. Las funciones desarrolladas permiten que distintos estudiantes, grupos o instituciones puedan aprovisionar laboratorios de manera independiente utilizando plantillas, roles y permisos diferenciados. Aunque la validación práctica se realizó en un entorno local monousuario (MiniONE), el diseño del complemento es compatible con despliegues OpenNebula más robustos que sí soportan multiusuario, multi-tenant y control de permisos granular. Esto permite que el complemento pueda integrarse en entornos educativos reales donde varios usuarios trabajan simultáneamente sin interferir entre sí.
------------------

## Requisitos del entorno: 

- MiniONE, VirtualBox, Ubuntu,etc.

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
----------
## Estructura del repositorio

- Copia_de_TFMlocal.ipynb – Notebook principal desarrollado en Google Colab.  
Este notebook contiene el mismo código que el archivo `TFMlocal.py` utilizado en Ubuntu durante la validación en MiniONE.

- TFMlocal.py – Versión del complemento ejecutada en Ubuntu dentro del entorno real (MiniONE + VirtualBox).  
Este archivo corresponde a la ejecución en modo simulación y pruebas de interacci{on con la API.

- logs/ – Carpeta de logs generados durante la validación (almacenados en Google Drive).

- README.md – Documentación del repositorio.

## Correspondencia entre archivos

- **TFMlocal.py** → Archivo ejecutado en Ubuntu dentro del entorno real (MiniONE).  
- **Copia_de_TFMlocal.ipynb** → Notebook equivalente usado en Google Colab para validación en modo simulación.

Ambos contienen la misma lógica del complemento, adaptada al entorno de ejecución.


----------------------------
##  Arquitectura del complemento

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

El complemento puede ejecutarse de dos maneras, dependiendo del entorno:

MODO_SIMULACION = True   # Simulación
MODO_SIMULACION = False  # Modo real

---

### 1. Ejecución desde el notebook (Google Colab o Jupyter)

**Pasos de ejecución:**

1. Abrir `Copia_de_TFMlocal.ipynb`.
2. Activar o desactivar el modo simulación modificando la variable:

```python
MODO_SIMULACION = True   # Simulación
MODO_SIMULACION = False  # Modo real

3. Si se usa modo real, ajustar las credenciales de oneadmin.

4. Ejecutar todas las celdas hasta llegar al flujo principal.

5. Ejecutar:
     ejecutar_complemento()

### 2. Ejecucion desde Ubuntu (archivo TFMlocal.py)
En el entorno Ubuntu + MiniONE, el complemento se ejecuta por defecto en modo simulación, ya que la variable:
python
**MODO_SIMULACION = True**,está definida así en el código original. Este modo permite validar la lógica, rutas, permisos y generación de logs dentro del entorno real (sandbox local) sin depender de la estabilidad de la API XML-RPC.

**Pasos de ejecucion**

  1. Abrir una terminal en la carpeta del archivo TFMlocal.py.
  2. Ejecutar el complemento directamente (no es necesario modificar nada para modo simulación):
  python3 TFMlocal.py
  3. Revisar los logs generados en la carpeta logs/ dentro del propio entorno local (sandbox).
      Estos logs corresponden a la validación real realizada en Ubuntu.

  Si bien el complemento incluye la opción de ejecutar en modo real (MODO_SIMULACION = False), este modo no fue utilizado en el       entorno MiniONE, ya que dicho entorno no garantiza la estabilidad necesaria para realizar llamadas reales a la API XML-RPC.

  MiniONE está diseñado para pruebas rápidas y funciona sobre VirtualBox, dependiendo de recursos locales. Esto puede provocar        reinicios del servicio, latencia o fallos de conexión.

  Por esta razón, la validación se realizó en modo simulación dentro del entorno real, garantizando trazabilidad y reproducibilidad   sin depender de la estabilidad de la API.

  El modo real queda disponible para entornos OpenNebula más robustos (por ejemplo, despliegues multi-nodo o instalaciones            completas), pero no se recomienda su uso en MiniONE.


-----


## Validación del complemento

La validación del complemento se realizó en dos entornos distintos, siguiendo una metodología incremental:
  1) Google Colab (entorno no real, sin acceso a la API XML-RPC)
  2) Ubuntu + MiniONE (entorno real, sandbox local)

Este enfoque permitió comprobar la lógica del complemento, su trazabilidad y su funcionamiento dentro de un entorno OpenNebula operativo, sin depender de infraestructura compleja.

## 1. Validación en Google Colab (modo simulación)

El notebook "Copia_de_TFMlocal.ipynb" se ejecutó en Google Colab, donde las restricciones de red impiden cualquier comunicación con la API XML-RPC de OpenNebula. Por esta razón, la validación se realizó exclusivamente en **modo simulación**.
En este modo, el sistema:

- Ejecuta el flujo principal del complemento

- Registra cada acción en consola

- Genera logs con timestamps

- Valida la lógica modular sin llamar a la API XML‑RPC

Esta validación permitió comprobar la coherencia del flujo, la modularidad y la trazabilidad del sistema.

## 2. Validación en Ubuntu + MiniONE (entorno real)
El complemento también fue ejecutado en un entorno real basado en:

- Ubuntu 22.04

- MiniONE (OpenNebula)

- VirtualBox

En este entorno, el complemento se ejecutó inicialmente en modo simulación, pero dentro de la infraestructura real, lo que permitió validar:

- Rutas y permisos del sistema

- Estructura de carpetas

- Generación de logs reales

- Funcionamiento del script en un entorno OpenNebula operativo

Posteriormente, se realizaron pruebas en modo real para validar la creación de plantillas, redes y máquinas virtuales desde la API.

Los logs generados en Ubuntu se encuentran almacenados en Google Drive y fueron mostrados durante la presentación del TFM. Están disponibles para revisión si el tribunal lo requiere.


## 3. Validación manual de roles
Finalmente, se verificó manualmente el funcionamiento de las máquinas virtuales creadas (roles atacante y objetivo) desde la interfaz de MiniONE, confirmando que:

- Las VMs se crean correctamente

- Pueden iniciarse desde la interfaz

- Operan como se espera en un escenario educativo tipo CTF

## Conclusión de la validación

La combinación de validación en Colab, validación en entorno real y verificación manual demuestra que el complemento es:

- Funcional

- Reproducible

- Portable

- Adecuado para entornos educativos con recursos limitados

##LIMITACIONES DEL ENTORNO Y LA VALIDACIÓN

Durante el desarrollo y validación del complemento se identificaron varias limitaciones técnicas derivadas del entorno disponible: - **Sin acceso al laboratorio cloud institucional (AWS/UOC):Esto obligó a realizar toda la validación en un entorno local reducido basado en Ubuntu + MiniONE.
- **Imposibilidad de utilizar la API XML-RPC de OpenNebula en la validación práctica:MiniONE es un entorno monousuario diseñado para pruebas rápidas y no garantiza la estabilidad necesaria para ejecutar llamadas reales a la API. Además, Google Colab no permite comunicación con redes locales ni con puertos personalizados, por lo que tampoco es posible acceder a la API desde ese entorno. Por estas razones, la validación se realizó íntegramente en **modo simulación**.

- **Dependencia de VirtualBox en modo NAT con port forwarding (Limitaciones del Hardware):
  * Esta configuración limita la exposición de servicios hacia el exterior y afecta la conectividad, impidiendo pruebas reales con     la API XML-RPC.
- **Escenario monousuario en MiniONE: No fue posible validar la lógica multiusuario del complemento, ya que MiniONE no soporta este     tipo de escenarios.
- **Ausencia de pruebas con herramientas de análisis avanzadas (Nmap, Wireshark, DVWA):Estas herramientas se consideraron como referencia conceptual, pero no se ejecutaron debido a las restricciones del entorno local.
Estas limitaciones no afectan la validez conceptual del complemento, sino que señalan áreas de mejora para futuras implementaciones en entornos OpenNebula más robustos.

