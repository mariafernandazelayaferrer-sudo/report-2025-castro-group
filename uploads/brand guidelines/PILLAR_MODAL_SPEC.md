# Modal de Detalle de Pilar — Spec

Componente expansivo que se despliega al clickar un KPI/botón de pilar (ej: **Água**, **Energia**, **Resíduos**) y muestra el desglose completo: gráficos, métricas y desgloses por categoría.

**Combina:**
- **Estética visual** → bloques azules con bubble charts + barras horizontales (referencia: `uploads/graficos 1.png`, `uploads/graficos 2.png`)
- **Layout / comportamiento** → modal centrado con header, grid de cards, scroll vertical (referencia: `uploads/gráficos.png`)

---

## 1. Comportamiento (trigger)

- En la home/dashboard hay tarjetas KPI o botones por pilar: `Energia`, `Água`, `Emissões`, `Resíduos`...
- Click en cualquiera → abre **modal overlay centrado** con backdrop oscuro (`rgba(15,15,18,0.92)` + `backdrop-filter: blur(10px)`)
- Animación de entrada: `opacity 0→1` + `translateY(20px → 0)`, duración ~300ms
- Cierra con: botón ✕, click en backdrop, tecla `Esc`
- Modal con `max-height: 86vh` y `overflow-y: auto` interno
- Ancho: `min(1100px, 92vw)`

---

## 2. Estructura del modal

```
┌──────────────────────────────────────────────────────────────┐
│  EYEBROW (mono)                                          ✕   │
│  02.2 — ENVIRONMENTAL · [PILLAR]                             │
│                                                              │
│  Título grande con KPI inline                                │
│  Consumo de água · 9.933,2 m³ · −14,5%                       │
│                                                              │
│  Subtítulo / contexto (1-2 líneas)                           │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌─── CARD AZUL PRINCIPAL (bubble chart) ───┐  ┌─ Card lateral ─┐
│  │                                          │  │ (negra o azul)  │
│  │   ●  bubble chart (azul + claro)         │  │ KPI grande      │
│  │       64,7%                              │  │ secundario      │
│  │   ●   ●                                  │  │                 │
│  │      23,0%                               │  │                 │
│  │                                          │  │                 │
│  │   Leyenda lateral con bullets            │  │                 │
│  └──────────────────────────────────────────┘  └─────────────────┘
│                                                              │
│  ┌──── CARD AZUL (barras horizontales) ────────────────────┐ │
│  │  A.  ████░░░░░░░░░  348,7 MWh  (11,3 kWh/m²)            │ │
│  │      ███░░░░░░░░░░  245,0 MWh   (7,9 kWh/m²)            │ │
│  │                                                          │ │
│  │  B.  ██████░░░░░░  651,3 MWh  (33,0 kWh/m²)             │ │
│  │      ████░░░░░░░░  458,9 MWh  (23,3 kWh/m²)             │ │
│  │                                                          │ │
│  │  Leyenda: A. Construção  B. Operação (CG)  ...          │ │
│  └──────────────────────────────────────────────────────────┘ │
│                                                              │
│  ┌─ Sub-card ──┐ ┌─ Sub-card ──┐ ┌─ Sub-card ──┐            │
│  │ POR TIPO     │ │ POR TIPO     │ │ POR TIPO     │           │
│  │ (barras      │ │ (barras      │ │ (barras      │           │
│  │  apiladas)   │ │  apiladas)   │ │  apiladas)   │           │
│  └──────────────┘ └──────────────┘ └──────────────┘           │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

---

## 3. Estilo visual — Sistema de colores

### Paleta (mantener consistencia con el design system)

| Token | Hex | Uso |
|---|---|---|
| `--blue-bg` | `#3F7EA8` | Fondo de cards de gráfico (azul medio) |
| `--blue-light` | `#A8C8DC` | Bubbles secundarias, barras secundarias |
| `--beige` | `#DCD9D0` | Bubble principal (fondo de bubble chart), barras de año anterior |
| `--ink` | `#1a1a1a` | Texto en cards beige, card oscura |
| `--white` | `#ffffff` | Texto sobre azul, sobre negro |
| `--orange` | `#E87A2E` | Eyebrows, deltas negativos/positivos según convención |
| `--gray-mid` | `#6b7280` | Texto secundario, labels |

### Card oscura (KPI secundario destacado)
- Fondo: `#1a1a1a`
- Texto: `#ffffff`
- Eyebrow naranja
- KPI gigante (~64px, weight 300)

---

## 4. Tipografía

| Elemento | Family | Size | Weight | Letterspacing | Notas |
|---|---|---|---|---|---|
| Eyebrow modal | mono (SF Mono / IBM Plex Mono) | 11px | 500 | 0.14em | uppercase, color naranja |
| Título modal | sans (Helvetica Neue) | 36–44px | 300 | -0.01em | KPI inline en mismo size |
| KPI inline (en título) | sans | 36–44px | 300 | — | el % delta puede ir en naranja |
| Subtítulo | sans | 13–14px | 400 | — | color gray-mid, max-width ~620px |
| Eyebrow de card | mono | 10px | 600 | 0.16em | uppercase, naranja en cards claras |
| Card KPI grande | sans | 32–64px | 300 | — | unidad inline en 14px gray |
| Leyenda / labels | sans | 11–12px | 500 | 0.02em | |
| Mono inline (valores) | mono | 11–12px | 500 | — | para datos tabulares |

---

## 5. Componentes de gráfico

### A. Bubble Chart (Distribuição por Atividade)
- Card de fondo `--blue-bg`, padding 32px, radius 4px
- 3 burbujas en relación de área proporcional a los %
- Bubble grande: `--beige` (color contenedor)
- Bubbles secundarias: `--blue-light`
- Texto del % dentro de cada bubble: `--ink` weight 500, 18–24px
- Leyenda lateral con `►` (triángulo) + título + bullets con dots de color
- Posición: bubbles flotando con `transform` para overlap orgánico

### B. Horizontal Bar Chart (Consumo por Atividade)
- Card de fondo `--blue-bg`, padding 32px
- Filas con label izquierdo (A. / B. / C.)
- Cada fila tiene 2 barras apiladas verticalmente (año actual + año anterior)
- Color barra año actual: `--beige`
- Color barra año anterior: `--blue-light`
- Extremos redondeados (`border-radius: 999px` o `stroke-linecap: round`)
- Valor numérico inline a la derecha: `348,7 MWh (11,3 kWh/m²)`
- Leyenda derecha con bullets de color

### C. Vertical Stacked Bar Chart (Consumo por Tipo)
- Card de fondo `--blue-bg`
- Pares de barras lado a lado (2024 vs 2025)
- Cada barra dividida en 2-3 segmentos (Eletricidade / Gasóleo / Total)
- Valores numéricos arriba y dentro de cada segmento
- Año debajo: `2024` / `2025` en weight 500

---

## 6. Layout responsive

| Breakpoint | Comportamiento |
|---|---|
| Desktop (>1024px) | Grid 2 columnas para top section, 3 cols para sub-cards |
| Tablet (768–1024px) | Grid 1 columna; sub-cards en 2 columnas |
| Mobile (<768px) | Stack vertical completo, modal ocupa 96vw |

---

## 7. API sugerida

```ts
interface PillarModalData {
  pillarId: 'energia' | 'agua' | 'emissoes' | 'residuos' | string;
  eyebrow: string;            // ej: "02.2 — ENVIRONMENTAL · ÁGUA"
  title: string;              // ej: "Consumo de água"
  kpi: {
    value: string;            // "9.933,2"
    unit: string;             // "m³"
    delta?: { value: string; positive: boolean }; // { value: "-14,5%", positive: true }
  };
  description: string;        // párrafo de contexto
  charts: ChartBlock[];       // bubble, barH, barVStacked, kpiBig...
  sideCards?: SideCard[];     // métricas secundarias (Operação OIC / Terceiros / Construção)
}

interface ChartBlock {
  type: 'bubble' | 'horizontalBars' | 'verticalStacked' | 'kpiCard';
  title: string;
  data: any;                  // shape depende del tipo
  legend?: { label: string; color: string }[];
}
```

---

## 8. Accesibilidad

- `role="dialog"` + `aria-modal="true"`
- Foco se mueve al modal al abrir, regresa al trigger al cerrar
- Atrapar tab dentro del modal mientras esté abierto
- `Esc` para cerrar
- Botón ✕ con `aria-label="Fechar"`

---

## 9. Datos que actualmente NO existen en el código

Listar los datasets que hay que añadir cuando Claude Code implemente esto:

- [ ] **Água**: total m³ 2024/2025, desglose por actividad (OIC/Terceiros/Construção), % reutilizada, top consumidores
- [ ] **Energia**: total MWh, desglose por actividad, por tipo (Eletricidade/Gasóleo), kWh/m² por activo
- [ ] **Emissões**: Scope 1+2 detalles, desglose por fuente
- [ ] **Resíduos**: total ton, por tipo (perigosos/não-perigosos), % reciclado

Cada pilar necesita su `PillarModalData` completo. Pedirle a Claude Code que use datos placeholder realistas si los reales no están disponibles.

---

## Resumen para Claude Code

> Implementa un modal de detalle de pilar que se abre al clickar las tarjetas KPI del overview. El modal usa la **estructura** del modal actual de Água (header con eyebrow mono + título grande con KPI inline, grid de cards, scroll interno) pero la **estética visual de los gráficos** debe ser azul (`#3F7EA8` fondo de cards) con bubbles/barras en beige (`#DCD9D0`) y azul claro (`#A8C8DC`), como las páginas de "Consumo de Energia por Atividade" del informe físico. Mantén el eyebrow naranja y la card secundaria oscura del modal original. Implementa al menos 3 tipos de gráfico: bubble chart, barras horizontales y barras verticales apiladas. Crea un dataset placeholder para cada pilar (Energia, Água, Emissões, Resíduos) siguiendo el shape `PillarModalData` descrito arriba.
