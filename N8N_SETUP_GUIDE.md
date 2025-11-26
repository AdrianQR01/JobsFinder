# Guía de Configuración de n8n

Esta guía te ayudará a configurar tu workflow de n8n para enviar datos procesados a tu backend.

## 📋 Requisitos Previos

- Tu backend debe estar corriendo en `http://localhost:3001`
- Si n8n está en la nube, necesitarás ngrok o exponer tu backend públicamente

## 🔧 Configuración del Workflow en n8n

### Paso 1: Estructura del Workflow

Tu workflow debe tener esta estructura:

```
[Webhook Trigger] → [Procesar CV] → [HTTP Request a tu Backend] → [Respond to Webhook]
```

### Paso 2: Configurar el nodo HTTP Request

Después de procesar el CV, añade un nodo **HTTP Request** con esta configuración:

#### Configuración Básica
- **Method**: `POST`
- **URL**: `http://localhost:3001/api/data`
  - ⚠️ Si n8n está en la nube, usa tu URL de ngrok: `https://tu-id.ngrok-free.app/api/data`

#### Body / Payload

Selecciona **JSON** y configura el body con los datos que procesaste:

```json
{
  "title": "{{ $json.jobTitle }}",
  "location": "{{ $json.location }}",
  "company": "{{ $json.company }}",
  "description": "{{ $json.description }}",
  "salary": "{{ $json.salary }}",
  "url": "{{ $json.url }}"
}
```

**Importante**: Asegúrate de que al menos uno de estos campos sea `location`, `localizacion` o `ubicacion` para que el backend lo detecte correctamente.

#### Headers (Opcional pero recomendado)

Añade este header:
```
Content-Type: application/json
```

### Paso 3: Verificar que funciona

#### En n8n:
1. Ejecuta el workflow manualmente
2. Verifica que el nodo HTTP Request devuelva `success: true`

#### En tu terminal (donde corre el backend):
Deberías ver algo como:
```
📥 Received data from n8n: {
  "title": "Senior Developer",
  "location": "Madrid",
  ...
}
✅ Data stored successfully. Total records: 1
   Title: Senior Developer
   Location: Madrid
```

### Paso 4: Configurar Respond to Webhook (Opcional)

Si quieres que n8n responda al cliente original, añade un nodo **Respond to Webhook** al final:

```json
{
  "success": true,
  "message": "CV procesado y guardado correctamente",
  "recordId": "{{ $('HTTP Request').item.json.id }}"
}
```

## 🌐 Si n8n está en la Nube

### Opción A: Usar ngrok (Recomendado para desarrollo)

1. Instala ngrok: `npm install -g ngrok`
2. Ejecuta: `ngrok http 3001`
3. Copia la URL que te da (ej: `https://abc123.ngrok-free.app`)
4. En n8n, usa: `https://abc123.ngrok-free.app/api/data`

### Opción B: Desplegar tu backend en la nube

Despliega tu backend en:
- Heroku
- Railway
- Render
- Vercel (con serverless functions)

Y usa esa URL en n8n.

## 🧪 Probar la Integración

### Test Manual desde n8n

En el nodo HTTP Request, haz clic en "Execute Node" para probar.

### Test desde tu navegador

Abre la consola del navegador y ejecuta:

```javascript
fetch('http://localhost:3001/api/data')
  .then(r => r.json())
  .then(data => console.log('Datos guardados:', data));
```

## 🔍 Troubleshooting

### Error: "Cannot connect to localhost"
- Si n8n está en la nube, no puede acceder a `localhost`
- Solución: Usa ngrok o despliega tu backend

### Error: "CORS"
- Tu backend ya tiene CORS habilitado
- Si persiste, verifica que el frontend esté en el mismo dominio o usa ngrok

### No veo los datos en el backend
- Verifica los logs del servidor
- Comprueba que el nodo HTTP Request en n8n se ejecute correctamente
- Revisa que el body JSON esté bien formado

## 📊 Endpoints Disponibles

Una vez que n8n envíe datos, puedes consultarlos:

- **Todos los datos**: `GET http://localhost:3001/api/data`
- **Filtrar por ubicación**: `GET http://localhost:3001/api/data?location=Madrid`
- **Filtrar por título**: `GET http://localhost:3001/api/data?title=Developer`
- **Ubicaciones únicas**: `GET http://localhost:3001/api/locations`
- **Títulos únicos**: `GET http://localhost:3001/api/titles`
- **Estadísticas**: `GET http://localhost:3001/api/stats`

## ✅ Checklist Final

- [ ] Backend corriendo en localhost:3001
- [ ] Nodo HTTP Request configurado en n8n
- [ ] URL correcta (localhost o ngrok)
- [ ] Body JSON con los campos correctos
- [ ] Test manual ejecutado con éxito
- [ ] Logs del backend muestran datos recibidos
