# MCP Map Servers - Colab Notebook

## Overview

Complete interactive implementation of MCP Map Servers using OpenAI Agents SDK and Model Context Protocol. Runs entirely in Google Colab with no local installation required.

## Quick Start

1. Upload `MCP_Map_Servers_Colab.ipynb` to Google Drive
2. Open with Google Colab
3. Add OpenAI API key to Colab Secrets (🔑 icon → `OPENAI_API_KEY`)
4. Run all cells: **Runtime → Run all**
5. Use the Gradio interface at the bottom

## Architecture

### **Model Context Protocol (MCP)**
MCP allows the OpenAI agent to discover and invoke custom tools exposed by map servers. Each tool is registered with a JSON schema defining its purpose and parameters, enabling the agent to intelligently orchestrate multiple operations.

### **Map Servers**

**🚗 CityNavigatorServer**
Handles geocoding and routing operations using OpenStreetMap data.

**Tools:**
- `forward_geocode(address)` - Converts street addresses to latitude/longitude coordinates
- `reverse_geocode(latitude, longitude)` - Converts coordinates to human-readable addresses
- `route(origin, destination, mode)` - Calculates routes with turn-by-turn directions (driving/walking/cycling)

**APIs:** Nominatim (geocoding), OSRM (routing)

**📍 PlacesExplorerServer**
Provides POI search and location discovery capabilities.

**Tools:**
- `search_poi(category, city)` - Finds places by category within a city (e.g., museums in Berlin)
- `search_nearby(latitude, longitude, category, radius_km)` - Discovers places near specific coordinates
- `suggest_places(query)` - Fuzzy search for place names and landmarks

**APIs:** Overpass (POI data), Photon (place search)

### **🤖 MapAssistant (OpenAI Agent)**
Orchestrates both servers using GPT-4o-mini with function calling. Automatically chains 2-5 tools to answer complex queries like "Find cafes near the Eiffel Tower and give me directions from the Louvre."

## 🛠️ Tools & APIs

**6 Tools (3 per server):**
- `forward_geocode`, `reverse_geocode`, `route`
- `search_poi`, `search_nearby`, `suggest_places`

**4 APIs:**
- Nominatim (geocoding), OSRM (routing)
- Overpass (POI data), Photon (search)

## 💡 Usage

### Example Queries:
```
"What are the coordinates of the Eiffel Tower?"
"Find cafes near the Eiffel Tower and give me directions from the Louvre"
"What's at coordinates 48.8584, 2.2945, find restaurants within 1km"
```
