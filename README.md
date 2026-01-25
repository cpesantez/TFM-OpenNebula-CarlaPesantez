# Complemento Técnico – TFM Carla Pesántez

## Tema del TFM
**Evaluación Comparativa de Soluciones Cyber Range en Nube Pública y Arquitecturas Híbridas, con Desarrollo de un Complemento Comunitario para OpenNebula**

Este repositorio contiene el complemento técnico desarrollado para el TFM, enfocado en la validación de un entorno local basado en OpenNebula MiniONE sobre Ubuntu 22.04 LTS, ejecutado en VirtualBox con configuración NAT + Port Forwarding.

El diseño está inspirado en la lógica modular de KYPO Cyber Range, adaptado a un sandbox local para pruebas controladas.


##  Objetivo del complemento técnico

El complemento implementa un flujo modular que permite:

- **Configurar un entorno local MiniONE**  
- **Autenticarse contra la API XML-RPC de OpenNebula**  
- **Instanciar máquinas virtuales desde plantillas**  
- **Simular configuración de red**  
- **Registrar eventos para trazabilidad y auditoría**  
- **Ejecutar un flujo principal tipo laboratorio CTF**  

Este código fue utilizado como parte del proceso de validación técnica del TFM.


## ⚙️ Arquitectura del complemento

El código está organizado en módulos:

1. **Configuración del entorno**  
2. **Autenticación XML-RPC**  
3. **Despliegue de máquinas virtuales**  
4. **Simulación de red**  
5. **Registro de eventos**  
6. **Flujo principal del complemento**  

El diseño permite añadir futuros entornos (por ejemplo, nube pública) sin modificar la lógica interna.



##  Modo Simulación

El complemento incluye un modo de simulación:

- **`MODO_SIMULACION = True`**  
  - No ejecuta llamadas reales a OpenNebula  
  - Imprime acciones  
  - Registra eventos  
  - Ideal para pruebas conceptuales

- **`MODO_SIMULACION = False`**  
  - Ejecuta llamadas reales a la API XML-RPC  
  - Requiere credenciales válidas de `oneadmin`

---

##  Estructura del repositorio

## Estructura del repositorio

- ** `Copia_de_TFMlocal.ipynb`** – Notebook principal desarrollado en Google Colab.  
Este notebook contiene el mismo código que el archivo `local.py` utilizado en Ubuntu durante la validación en MiniONE.

- ** `TFMlocal.py`** – Versión del complemento ejecutada en Ubuntu dentro del entorno real (MiniONE + VirtualBox).  
Este archivo corresponde a la ejecución en modo simulación y modo real dentro de la infraestructura local.

- ** `logs/`** – Carpeta de logs generados durante la validación (almacenados en Google Drive).

- **`README.md`** – Documentación del repositorio.


---

##  Ejecución del complemento

1. Abrir el notebook en Google Colab o Jupyter.  
2. Ajustar credenciales reales de `oneadmin` si se desactiva el modo simulación.  
3. Ejecutar la función `ejecutar_complemento()` para iniciar el flujo.
4. 

-----


## Validación del complemento
La validación del complemento se realizó en dos entornos distintos, siguiendo una metodología incremental:

## 1. Validación en Google Colab (modo simulación)
El notebook Copia_de_TFMlocal.ipynb contiene la ejecución del complemento en modo simulación, debido a las restricciones de red de Colab.
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
