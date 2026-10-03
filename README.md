# ⚡ CTP — Calculadora de Planta

App web (single-file, sin dependencias) para calcular **qué equipos puedes conectar a tu planta eléctrica (generador)** y cuánto tiempo aguantarán, con **valores reales de consumo** y **picos de arranque** de los motores.

🔗 **Demo en vivo:** https://aurenox-global.github.io/ctp/

---

## ✨ Qué hace

- **Configura la planta:** potencia (W), energía disponible (Wh) y margen de seguridad (%) — recomendado 80 %.
- **Catálogo real de equipos** (~40 aparatos) agrupado por categorías: 💡 Iluminación, 🌡️ Clima, 🍳 Cocina, 💻 Electrónicos, 🧺 Lavado y limpieza, 💧 Bombas y motores y 🔨 Herramientas.
- **Perfiles rápidos:** 🏠 Básico, 🏡 Casa, 💻 Oficina (teletrabajo), 🚨 Emergencia (apagón), 🍳 Cocina y limpiar todo.
- **Equipos personalizados:** añade cualquier aparato con su potencia.
- **Análisis en tiempo real:**
  - **Consumo diario** (kWh/día) según las horas de uso de cada equipo.
  - **Pico de arranque** (surge) — la potencia extra que demandan los motores al arrancar.
  - **Autonomía** (continua y según uso diario).
  - Potencia usada vs. disponible, con barra de progreso y semáforo de estado.
- **Aviso inteligente:** si el pico de arranque supera la planta, te avisa y recomienda la potencia mínima necesaria.
- **Persistencia:** guarda tu configuración en `localStorage` (nada sale del navegador).
- **Tema claro/oscuro** con botón 🌓 y diseño glassmorphism responsive.

## 🚀 Uso

No requiere build ni instalación. Abre `index.html` en el navegador o entra a la demo:

```
https://aurenox-global.github.io/ctp/
```

### Local

```bash
git clone https://github.com/aurenox-global/ctp.git
cd ctp
# abre index.html directamente, o sirve el directorio:
python3 -m http.server 8000
# → http://localhost:8000
```

## 🔌 Sobre los datos "reales"

Cada equipo del catálogo trae tres datos orientativos basados en valores típicos de placa/etiqueta energética:

| Campo | Descripción |
|---|---|
| `watts` | Rango de **potencia en marcha** [mín, típico, máx] en W |
| `surge` | **Pico de arranque** en W (solo equipos con motor) |
| `hours` | **Horas de uso** típicas al día |

> ⚠️ **El pico de arranque importa.** Un motor (nevera, aire acondicionado, bomba, lavadora, compresor) consume **2-4× más potencia durante 1-3 s** al arrancar. Una planta que cubre la potencia en marcha pero no el pico **no arrancará esos equipos**.
>
> Ejemplos de referencia: nevera ≈ 150 W en marcha / **1200 W al arrancar** · aire acondicionado split 12000 BTU ≈ 1200 W / **3600 W** · bomba 1 HP ≈ 750 W / **2200 W**.

Los valores son orientativos; ajústalos según la placa de cada aparato.

## 🧮 Cómo calcula

- **Potencia usada** = Σ `potencia × cantidad` (equipos en marcha).
- **Disponible** = `potencia de planta × margen de seguridad / 100`.
- **Pico de arranque** = `potencia usada + mayor pico extra de un solo motor` (`surge − watts`). Se asume que los motores arrancan de uno en uno.
- **Consumo diario** = Σ `potencia × cantidad × horas de uso`.
- **Autonomía continua** = `energía Wh / potencia usada` (todo encendido a la vez).
- **Autonomía de uso diario** = `energía Wh / consumo diario`.
- **Estado:** ✅ OK · ⚠️ Cerca (>85 % del disponible) · ⚠️ Arranque (pico > planta) · ⛔ Sobrecarga.

## 🛠️ Tecnología

- **HTML + CSS + JavaScript vanilla** — sin frameworks, sin dependencias, un solo archivo `index.html`.
- **GitHub Pages** para el hosting.

## 📁 Estructura

```
ctp/
├── index.html   # toda la app (UI + estilos + lógica)
└── README.md
```

## 🌐 Despliegue

Servido con **GitHub Pages** desde la rama `main`, ruta `/`. Cualquier push a `main` actualiza la web automáticamente.

---

© aurenox-global · Calculadora de Planta
