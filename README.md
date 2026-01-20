# TFM-OpenNebula-CarlaPesantez

Complemento técnico desarrollado como parte del Trabajo de Fin de Máster (TFM) en ciberseguridad y privacidad.  
Este proyecto implementa un entorno local de validación basado en OpenNebula MiniONE sobre Ubuntu 22.04 LTS, ejecutado en VirtualBox con configuración NAT + Port Forwarding.

## 🧩 Objetivo

Diseñar y probar un complemento técnico que permita simular el despliegue de máquinas virtuales, inspirado en la lógica modular de KYPO Cyber Range, adaptado a un entorno local.

## ⚙️ Componentes principales

- **Configuración del entorno** (`local_minione`)
- **Autenticación vía API XML-RPC**
- **Despliegue de máquinas virtuales desde plantilla**
- **Simulación de configuración de red**
- **Registro de eventos para trazabilidad**
- **Flujo principal de ejecución (ejemplo tipo CTF)**

## 🧪 Modo Simulación

El código incluye un modo de simulación (`MODO_SIMULACION = True`) que permite validar la lógica sin ejecutar llamadas reales a la API de OpenNebula.

## 📁 Estructura del repositorio

- `TFMlocal.ipynb`: cuaderno principal desarrollado en Google Colab
- `logs/eventos_complemento.log`: archivo de registro de eventos
- `README.md`: descripción del proyecto
- (Opcional) `docs/`: documentación complementaria o resumen del TFM

## 🚀 Ejecución

1. Abrir el notebook en Google Colab o Jupyter.
2. Configurar credenciales reales de `oneadmin` si se desactiva el modo simulación.
3. Ejecutar la función `ejecutar_complemento()` para iniciar el flujo.

---

Este repositorio sirve como evidencia técnica y trazabilidad del desarrollo realizado en el TFM.
