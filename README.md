# ⚡ CTP — Calculadora de Planta

App web (single-file, sin dependencias) para calcular **qué equipos puedes conectar a tu planta eléctrica** y cuánto tiempo aguantarán según la potencia y la energía disponibles.

🔗 **Demo en vivo:** https://aurenox-global.github.io/ctp/

---

## ✨ Qué hace

- **Configura la planta:** potencia (W), energía disponible (Wh) y margen de seguridad (%) — recomendado 80 %.
- **Catálogo de equipos** agrupado por categorías: 💡 Iluminación, 🌡️ Clima, 🍳 Cocina, 💻 Electrónicos, 🧹 Limpieza y 💧 Otros.
- **Perfiles rápidos:** carga un set predefinido (🏠 Básico, 🏡 Casa) o límpialo todo.
- **Equipos personalizados:** añade cualquier aparato con su propio nombre y potencia.
- **Cálculo en tiempo real:**
  - Potencia usada vs. disponible (con barra de progreso y semáforo de estado).
  - ⏱️ Autonomía estimada (horas) según los Wh disponibles.
  - Aviso visual cuando te pasas de la capacidad.
- **Persistencia:** guarda tu configuración y equipos en `localStorage` (nada se envía a ningún servidor).
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

## 🧮 Cómo calcula

- **Potencia usada** = suma de `potencia × cantidad` de cada equipo encendido.
- **Disponible** = `potencia de planta × margen de seguridad / 100`.
- **Autonomía** = `energía disponible (Wh) / potencia usada (W)`.
- **Estado:** ✅ OK por debajo del margen · ⚠️ cerca del límite · ⛔ sobrepasado.

> Los valores del catálogo son orientativos; ajusta según la placa de cada aparato.

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
