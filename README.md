# scrapThaCV

Aplicación web moderna para subir y procesar CVs con integración a N8N.

## 🚀 Inicio Rápido

### Prerequisitos
- Node.js (v18 o superior)
- npm o pnpm

### Instalación

1. **Clona el repositorio:**
   ```bash
   git clone <tu-repositorio>
   cd scrapThaCV
   ```

2. **Instala las dependencias:**
   ```bash
   npm install
   ```

3. **Configura las variables de entorno:**
   ```bash
   cp .env.example .env
   ```
   
   Luego edita `.env` y agrega tu URL de webhook de N8N. Ver [SECURITY_SETUP.md](./SECURITY_SETUP.md) para más detalles.

4. **Inicia el servidor de desarrollo:**
   ```bash
   npm run dev
   ```

5. **Abre tu navegador en:** `http://localhost:4321`

## 📁 Estructura del Proyecto

```
scrapThaCV/
├── src/
│   ├── components/     # Componentes de Astro
│   ├── layouts/        # Layouts de página
│   ├── pages/          # Páginas de la aplicación
│   └── styles/         # Estilos globales
├── public/             # Archivos estáticos
├── .env.example        # Plantilla de variables de entorno
└── SECURITY_SETUP.md   # Guía de configuración de seguridad
```

## 🔒 Seguridad

Este proyecto utiliza variables de entorno para proteger información sensible. **NUNCA** subas el archivo `.env` a Git.

Para más información sobre la configuración segura, consulta [SECURITY_SETUP.md](./SECURITY_SETUP.md).

## 🛠️ Tecnologías

- **Astro** - Framework web moderno
- **TypeScript** - Tipado estático
- **Tailwind CSS** - Framework de CSS
- **N8N** - Automatización de workflows

## 📝 Scripts Disponibles

- `npm run dev` - Inicia el servidor de desarrollo
- `npm run build` - Construye la aplicación para producción
- `npm run preview` - Previsualiza la build de producción

## 🤝 Contribuir

1. Haz fork del proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

**Importante:** Asegúrate de no incluir credenciales en tus commits.

## 📄 Licencia

Este proyecto es privado y confidencial.
"# JobsFinder" 
