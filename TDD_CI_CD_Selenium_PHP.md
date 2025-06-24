# Clase de Profundización: TDD + CI/CD + Selenium en PHP

## 📘 Introducción

En esta clase profundizaremos en el enfoque **TDD (Desarrollo Guiado por Pruebas)** dentro de un proceso de desarrollo moderno. Integraremos este enfoque con herramientas de automatización como **PHPUnit**, **Selenium** y **GitHub Actions**, dentro de un flujo **CI/CD** que garantice calidad desde la codificación hasta la entrega.

---

## 🎯 Objetivos de Aprendizaje

Al finalizar esta clase, el estudiante será capaz de:

- Explicar los principios y beneficios del desarrollo guiado por pruebas (TDD).
- Implementar pruebas unitarias en PHP utilizando PHPUnit.
- Realizar pruebas funcionales automáticas con Selenium WebDriver.
- Integrar ambas pruebas en un flujo automatizado de CI/CD usando GitHub Actions.

---

## 🧠 1. Fundamentos Teóricos

### 🔁 ¿Qué es TDD?

**TDD (Test-Driven Development)** es una metodología ágil que propone:

1. **Escribir primero las pruebas**, antes del código que las hace pasar.
2. **Codificar la funcionalidad mínima** para que la prueba pase.
3. **Refactorizar el código**, manteniendo las pruebas funcionando.

#### Ciclo Red - Green - Refactor

```plaintext
Red     →     Green      →     Refactor
(Falla)      (Funciona)         (Mejora)
```

Este enfoque permite:

- Tener siempre una **base de pruebas confiables**.
- Diseñar código más limpio y **menos acoplado**.
- **Prevenir errores antes de que ocurran** en producción.

---

### 🧪 Tipos de pruebas

| Tipo         | Objetivo                                 | Herramienta sugerida |
|--------------|------------------------------------------|-----------------------|
| Unitaria     | Validar funciones/métodos aislados       | PHPUnit               |
| Integración  | Verificar interacción entre módulos      | PHPUnit               |
| Funcional/UI | Simular flujo real del usuario           | Selenium              |

---

### 📦 PHPUnit: pruebas unitarias en PHP

PHPUnit es el estándar de facto para pruebas en PHP. Permite crear suites de prueba, assertions y mocks.

#### Ejemplo simple:

```php
use PHPUnit\Framework\TestCase;

class CalculadoraTest extends TestCase
{
    public function testSuma()
    {
        $this->assertEquals(4, 2 + 2);
    }
}
```

---

### 🌐 Selenium: automatización del navegador

Selenium permite automatizar interacciones con el navegador (como si fuera un usuario real):

- Completar formularios
- Click en botones
- Verificación de contenido
- Validación de flujos de login, CRUD, etc.

#### Selenium con PHP (vía `php-webdriver`)

```php
use Facebook\WebDriver\Remote\RemoteWebDriver;
use Facebook\WebDriver\WebDriverBy;

$driver = RemoteWebDriver::create("http://localhost:4444/wd/hub", DesiredCapabilities::chrome());
$driver->get("http://localhost:8000/login.php");

$driver->findElement(WebDriverBy::id("email"))->sendKeys("admin@demo.com");
$driver->findElement(WebDriverBy::id("password"))->sendKeys("123456");
$driver->findElement(WebDriverBy::id("submit"))->click();

$this->assertStringContainsString("Panel", $driver->getTitle());
$driver->quit();
```

---

### 🔄 CI/CD con GitHub Actions

GitHub Actions permite:

- Ejecutar pruebas automáticamente en cada `push` o `pull request`.
- Verificar que las pruebas unitarias y funcionales pasen.
- Automatizar despliegues (CD).

#### Flujo típico:

```
Push → Ejecutar PHPUnit → Ejecutar Selenium → Notificar/Desplegar
```

---

### 📁 Ejemplo de Workflow

```yaml
name: CI con PHPUnit y Selenium

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      selenium:
        image: selenium/standalone-chrome
        ports:
          - 4444:4444

    steps:
      - uses: actions/checkout@v3

      - name: Configurar PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: '8.2'

      - name: Instalar dependencias
        run: composer install

      - name: Ejecutar pruebas unitarias
        run: ./vendor/bin/phpunit tests/unit

      - name: Ejecutar pruebas funcionales
        run: ./vendor/bin/phpunit tests/functional
```

---

## 💻 Parte Práctica

### Actividad:

1. Implementar 2 pruebas unitarias con PHPUnit para funciones clave del sistema.
2. Crear 1 prueba funcional con Selenium que:
   - Ingrese a la aplicación
   - Realice login correcto
   - Valide el acceso a una sección protegida
3. Configurar `ci.yml` para correr todo automáticamente.

---

## 📤 Entrega

Cada grupo deberá entregar:

- Carpeta `tests/` con pruebas unitarias y funcionales.
- Archivo `.github/workflows/ci.yml` funcional.
- Evidencia en GitHub Actions (captura o link).
- Documento `.md` breve con:
  - Descripción del flujo de trabajo.
  - Problemas encontrados y cómo los resolvieron.

---

## 📚 Recursos Recomendados

- [PHPUnit - Sitio oficial](https://phpunit.de/)
- [GitHub Actions para PHP](https://github.com/shivammathur/setup-php)
- [php-webdriver (Selenium en PHP)](https://github.com/php-webdriver/php-webdriver)
- [Docker Selenium](https://github.com/SeleniumHQ/docker-selenium)
- [Testing con TDD - Artículo en español](https://apuntes.de/testing/tdd/)
