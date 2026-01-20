# Complemento Técnico – TFM Carla Pesántez

## Tema del TFM
**Evaluación Comparativa de Soluciones Cyber Range en Nube Pública y Arquitecturas Híbridas, con Desarrollo de un Complemento Comunitario para OpenNebula**

Este repositorio contiene el complemento técnico desarrollado para el TFM, enfocado en la validación de un entorno local basado en OpenNebula MiniONE sobre Ubuntu 22.04 LTS, ejecutado en VirtualBox con configuración NAT + Port Forwarding.

El diseño está inspirado en la lógica modular de KYPO Cyber Range, adaptado a un sandbox local para pruebas controladas.

---

## 🧩 Objetivo del complemento técnico

El complemento implementa un flujo modular que permite:

- **Configurar un entorno local MiniONE**  
- **Autenticarse contra la API XML-RPC de OpenNebula**  
- **Instanciar máquinas virtuales desde plantillas**  
- **Simular configuración de red**  
- **Registrar eventos para trazabilidad y auditoría**  
- **Ejecutar un flujo principal tipo laboratorio CTF**  

Este código fue utilizado como parte del proceso de validación técnica del TFM.

---

## ⚙️ Arquitectura del complemento

El código está organizado en módulos:

1. **Configuración del entorno**  
2. **Autenticación XML-RPC**  
3. **Despliegue de máquinas virtuales**  
4. **Simulación de red**  
5. **Registro de eventos**  
6. **Flujo principal del complemento**  

El diseño permite añadir futuros entornos (por ejemplo, nube pública) sin modificar la lógica interna.

---

## 🧪 Modo Simulación

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

## 📁 Estructura del repositorio

- **`TFMlocal.ipynb`** – Notebook principal desarrollado en Google Colab  
- **`logs/eventos_complemento.log`** – Registro de eventos del complemento  
- **`README.md`** – Documentación del repositorio  

---

## 🚀 Ejecución del complemento

1. Abrir el notebook en Google Colab o Jupyter.  
2. Ajustar credenciales reales de `oneadmin` si se desactiva el modo simulación.  
3. Ejecutar la función `ejecutar_complemento()` para iniciar el flujo.  

---

Este repositorio sirve como evidencia técnica y trazabilidad del desarrollo realizado en el TFM.
