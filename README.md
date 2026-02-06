# Plataforma-Digital-EPURA
This project provides an advanced 3D mapping interface for the Epura Observatory, featuring geographic data visualization with interactive filters, thematic layers, and detailed property information. Built with MapLibre GL JS and MapTiler, it enables researchers and users to explore urban patterns, vacant lots, and property data.

DEMONSTRATION: portfolio-seven-umber-ldnh0lh5ob.vercel.app/project/plataforma-epura
# 🗺️ Epura Observatory - Interactive Map Platform

A web-based interactive mapping platform for urban analysis and research visualization, focusing on the Cuiabá metropolitan area in Mato Grosso, Brazil.

## 📋 Overview

Features

- **3D Interactive Map** - Fully navigable 3D terrain with customizable pitch and bearing
- **Multiple GeoJSON Layers** - PEDRA90 parcels, perimeter boundaries, streams, and contours
- **Dynamic Filtering** - Real-time filtering by property type, ownership, and characteristics
- **Hover Effects** - Visual feedback on geographic features
- **Popup Information** - Detailed property data including ownership, IPTU status, and area
- **Responsive Sidebar** - Collapsible interface with thematic research categories
- **Custom Styling** - Color-coded visualization by property types and land use

## 📁 Project Structure

```
site 0.1/
├── mapa-3d.html           # Main map application
├── mapagio.html           # Simplified 3D map version
├── scripts.js             # Core JavaScript logic (460 lines)
├── styles.css             # Custom styling (465 lines)
├── README.md              # Project documentation (Portuguese)
├── README-EN.md           # Project documentation (English)
├── data/                  # Geographic data files
│   ├── CONTORNO.geojson   # Boundary contours
│   ├── PEDRA90.geojson    # Property parcels (1575 lines)
│   ├── PEDRA90.qmd        # Metadata
│   ├── PERIMETRO.geojson  # Perimeter lines
│   ├── PERIMETRO.qmd      # Metadata
│   ├── RIBEIRAO.geojson   # Stream/river data
│   └── RIBEIRAO.qmd       # Metadata
├── design/                # Visual assets (logos, icons)
├── modules/               # JavaScript modules
│   └── mapa.js           # (Reserved for modularization)
└── .github/
    └── copilot-instructions.md
```

## 🛠️ Technical Stack

- **MapLibre GL JS** - Open-source mapping library
- **MapTiler API** - Custom map tiles and styling
- **Vanilla JavaScript** - No frameworks, pure JS
- **CSS3** - Advanced styling with transitions and transforms
- **GeoJSON** - Standard geographic data format

## 📍 Map Configuration

### Default View
- **Center**: UFMT Campus, Cuiabá (-56.065147, -15.607951)
- **Initial Zoom**: 15
- **Pitch**: 60° (3D angle)
- **Min Zoom**: 12
- **Max Bounds**: Restricted to Cuiabá/Várzea Grande area

### Predefined Locations
- **Cuiabá**: [-56.1, -15.6], zoom 12
- **Pedra 90**: [-55.95, -15.64], zoom 15
- **Coxipó**: [-56.059, -15.626], zoom 15

## 🎨 Geographic Layers

### 1. PEDRA90 (Property Parcels)
Interactive polygon layer with detailed property information:

**Available Properties:**
- `TIPO` - Property type classification
- `PROPIETARIO` - Owner name
- `CPF` - Brazilian tax ID
- `PROPI` - Owner type (PF/PJPUBLICA/PJPRIV)
- `IPTU_S_OU_N` - Property tax payment status
- `IPTU_QNTS_ANOS` - Years of IPTU payment
- `REAIS` - Value in Brazilian Reais
- `AREA` - Parcel area in m²
- `SOMA_AREA` - Total aggregated area

**Property Type Classifications:**
- **APP** - Área de Proteção Permanente (Permanent Protection Area)
- **ELNC** - Espaço Livre Não Configurado (Unconfigured Open Space)
- **EST** - Estacionamento (Parking)
- **GNP** - Gleba Não Parcelada (Unparceled Land)
- **LNE** - Lote Não Edificado (Unbuilt Lot)
- **SEL** - Sistema de Espaço Livre (Open Space System)
- **SUB** - Subutilizado (Underutilized)
- **EDF** - Edificado (Built)

**Features:**
- Interactive filters by property type
- Color-coded visualization
- Configurable outlines
- Click-to-view detailed information

### 2. CONTORNO (Contour Lines)
- Style: Red (#ff7a7a)
- Hover effect enabled
- Buffer area for improved interaction

### 3. RIBEIRAO (Streams/Rivers)
- Style: Blue (#37c0ff)
- Hover effect enabled
- Vertical offset (-20) for better visibility
- Toggle visibility control

### 4. PERIMETRO (Perimeter)
- Style: Purple (#dbaeec), dashed line
- Marks study area boundaries

## 🎯 User Interface

### Fixed Sidebar
**Specifications:**
- Position: Left side
- Width: 151px
- Background: #F7F4F1 (light beige)
- Responsive behavior with smooth transitions

**Components:**
- Observatory logo/branding
- Research categories button (Pesquisas)
- Publications button (Produções)
- Municipality quick navigation
- Dynamic information panel

### Interactive Popups
**Features:**
- Auto-positioning based on sidebar
- Dynamic content from metadata
- Image and link support
- Expand/collapse sections
- Close button with smooth animations

### Filter System
- Checkbox controls for PEDRA90 types
- Toggle switches for layer visibility
- Persistent state management
- Real-time map updates

## 💻 Core Functions

### Layer Control
```javascript
// Toggle layer visibility
map.setLayoutProperty(layerId, 'visibility', 'visible'|'none');

// Apply filters
map.setFilter(layerId, ['any', ['==', ['get', 'TIPO'], value]]);
```

### Hover Effects
```javascript
addHoverEffect(hoverId, visibleId, translateProp);
```
Adds visual feedback with translation effects on hover.

### Popup Display
```javascript
showGenericPopup(layerId, event);
```
Shows contextual information for clicked features.

### Navigation
```javascript
zoomMapa(center, zoom);
```
Animates camera to specified coordinates and zoom level.

## 🔄 Initialization Flow

1. Load MapTiler base map
2. Initialize UI components (`initUI()`)
3. Load GeoJSON layers from `data/` directory
4. Configure event listeners and hover effects
5. Build filter controls and legends
6. Apply initial visibility and style settings

## 🎨 Customization

### Styling
- Main styles: `styles.css`
- Layer colors defined in map paint properties
- CSS variables for theming (e.g., `--sidebar-width`)

### Configuration
- Map settings: Beginning of `scripts.js`
- API key: `const apiKey` in scripts
- Popup metadata: `popupMetadata` object
- Type legends: `tipoLegenda` object

### Adding New Features
1. **New property types**: Add to `tipoLegenda`
2. **New popup content**: Update `popupMetadata`
3. **New layers**: Follow GeoJSON loading pattern
4. **Hover effects**: Use `translate` property for offset

## 📦 Dependencies

### External Libraries
- **MapLibre GL JS** - https://unpkg.com/maplibre-gl/dist/maplibre-gl.js
- **MapLibre CSS** - https://unpkg.com/maplibre-gl/dist/maplibre-gl.css

### API Keys
- MapTiler API key required (included in code)

### Browser Requirements
- Modern browser with WebGL support
- JavaScript enabled
- Internet connection for tile loading

## 🖱️ User Interactions

### Map Navigation
- **Pan**: Click and drag
- **Zoom**: Mouse wheel or pinch gesture
- **Rotate**: Right-click + drag (or Ctrl + drag)
- **Tilt**: Shift + drag

### Feature Interaction
- **Click parcels**: View detailed property information
- **Hover lines**: Visual highlight effect
- **Filter checkboxes**: Show/hide property types
- **Sidebar icons**: Open thematic research panels

## 📊 Data Sources

The project includes geographic data focusing on:
- Urban vacant lots and underutilized properties
- Property ownership and tax compliance patterns
- Environmental protection areas
- Metropolitan boundary definitions
- Hydrographic features (streams and rivers)

## 🔮 Future Development

Potential enhancements:
- Modularize JavaScript code (use `modules/mapa.js`)
- Add time-series data visualization
- Implement data export functionality
- Create print-friendly map views
- Optimize for mobile devices
- Add search functionality for addresses/parcels
- Include statistical dashboards

## 💡 Development Tips

- Property type filters are based on the `TIPO` attribute in GeoJSON
- Hover effects use CSS `translate` for smooth displacement
- All popups require entries in `popupMetadata` for proper rendering
- Layer IDs must match between source, layer, and filter references
- GeoJSON files are loaded asynchronously on map load event

## 📄 License

Part of the Epura Observatory research initiative for urban analysis.

## 👥 Credits

**Epura Observatório**  
Urban research and spatial analysis platform  
Cuiabá, Mato Grosso, Brazil

---

For Portuguese documentation, see `README.md`
