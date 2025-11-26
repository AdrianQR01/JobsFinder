# 🔒 Configuración de Seguridad

Este proyecto usa variables de entorno para proteger información sensible como URLs de webhooks y API keys.

## 📋 Configuración Inicial

1. **Copia el archivo de ejemplo de variables de entorno:**
   ```bash
   cp .env.example .env
   ```

2. **Edita el archivo `.env` con tus credenciales reales:**
   - Abre `.env` en tu editor
   - Reemplaza `https://your-n8n-instance.app.n8n.cloud/webhook-test/your-webhook-id` con tu URL real de webhook de N8N

3. **IMPORTANTE:** 
   - ⚠️ **NUNCA** subas el archivo `.env` a Git
   - El archivo `.env` ya está en `.gitignore` y no se subirá
   - Solo comparte el archivo `.env.example` en el repositorio

## 🔐 Variables de Entorno

### `PUBLIC_N8N_WEBHOOK_URL`
URL del webhook de N8N para procesar los CVs subidos.

**Formato:** `https://[tu-instancia].app.n8n.cloud/webhook-test/[tu-webhook-id]`

## 🚀 Para Otros Desarrolladores

Si clonas este repositorio:

1. Crea tu propio archivo `.env` basado en `.env.example`
2. Solicita las credenciales al administrador del proyecto
3. Nunca compartas tus credenciales en mensajes públicos o commits

## ✅ Verificación

Para verificar que todo está configurado correctamente:

1. Asegúrate de que existe el archivo `.env` en la raíz del proyecto
2. Verifica que `.env` contiene `PUBLIC_N8N_WEBHOOK_URL` con una URL válida
3. Ejecuta `npm run dev` - si hay un error sobre variables no configuradas, revisa tu `.env`
