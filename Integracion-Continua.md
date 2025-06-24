# Clase de Profundización: DevOps y CI/CD con GitHub Actions

## 📘 Objetivos de Aprendizaje

Al finalizar la clase, los estudiantes serán capaces de:

- Comprender los conceptos de DevOps, CI y CD.
- Configurar flujos de integración continua utilizando GitHub Actions.
- Automatizar pruebas y despliegue para una aplicación propia (login con 2FA o sistema de gestión de personal).

---

## 🕒 Duración: 3 horas (1 hora teórica + 2 horas práctica)

---

## 🧠 Parte 1: Teoría (60 min)

### 🔧 ¿Qué es DevOps?

- DevOps es una combinación de **prácticas culturales, metodologías y herramientas**.
- Su objetivo es **automatizar y mejorar** la colaboración entre desarrollo y operaciones.
- Permite **entregar software de forma más rápida, segura y continua**.

### 🔄 ¿Qué es CI/CD?

| Término               | Significado                                                                 |
|----------------------|------------------------------------------------------------------------------|
| **CI** - Integración Continua | Automatizar la validación (compilación, pruebas) de cada cambio en el código.     |
| **CD** - Entrega / Despliegue Continua | Automatizar la entrega/despliegue en entornos de prueba o producción. |

### 🔧 ¿Qué es GitHub Actions?

- Es una **plataforma de automatización integrada** en GitHub.
- Permite definir **workflows** que se ejecutan ante eventos como `push`, `pull_request`, `release`, etc.
- Cada flujo se define como archivo `.yml` dentro de `.github/workflows/`.

---

### 🧱 Estructura básica de un workflow

```yaml
name: CI Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout del código
        uses: actions/checkout@v3

      - name: Instalar dependencias
        run: npm install

      - name: Ejecutar pruebas
        run: npm test
```
🧪 Parte 2: Práctica Guiada (120 min)
🔍 Contexto del Proyecto
Aplicar DevOps a uno de los siguientes proyectos del curso:

Sistema de login con 2FA

Sistema de gestión de personal

El proyecto debe tener:

Al menos una prueba unitaria funcional.

Un package.json, composer.json o similar para instalar dependencias.

🛠️ Actividad paso a paso
1. Crear el directorio de configuración
```bash

mkdir -p .github/workflows
touch .github/workflows/ci.yml
```
2. Crear un archivo YAML de CI
Ejemplo básico para Node.js:

```yaml

name: Node.js CI

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm install
      - run: npm test
```
Para proyectos PHP, usar setup-php, y para Python, usar setup-python.

✅ Validar ejecución del workflow
Hacer git add, commit y push al repositorio.

Ir a la pestaña Actions de GitHub.

Verificar que el workflow se ejecuta correctamente.

📛 Agregar badge al README

![CI](https://github.com/usuario/repositorio/actions/workflows/ci.yml/badge.svg)
