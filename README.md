# 📧 MsNotificaciones

**Microservicio de Notificaciones por Email** - Una API REST construida con .NET para el envío automatizado de notificaciones de eventos utilizando SendGrid.

[![.NET](https://img.shields.io/badge/.NET-6.0-blue.svg)](https://dotnet.microsoft.com/)
[![SendGrid](https://img.shields.io/badge/SendGrid-Email%20Service-00D4FF.svg)](https://sendgrid.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 📋 Tabla de Contenidos

- [Descripción](#-descripción)
- [Características](#-características)
- [Tecnologías](#-tecnologías)
- [Prerrequisitos](#-prerrequisitos)
- [Instalación](#-instalación)
- [Configuración](#-configuración)
- [Uso](#-uso)
- [API Endpoints](#-api-endpoints)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Contribuir](#-contribuir)
- [Licencia](#-licencia)

## 🎯 Descripción

MsNotificaciones es un microservicio especializado en el envío de notificaciones por email para eventos. Diseñado específicamente para gestionar modificaciones de eventos, utiliza plantillas predefinidas de SendGrid para garantizar un formato consistente y profesional en todas las comunicaciones.

### Caso de Uso Principal
- **Notificación de modificaciones de eventos**: Cuando un evento cambia de fecha, ubicación o detalles, el sistema envía automáticamente una notificación personalizada a los participantes registrados.

## ✨ Características

- 🚀 **API REST rápida y ligera** construida con ASP.NET Core 6
- 📧 **Integración completa con SendGrid** para entrega confiable de emails
- 🎨 **Soporte para plantillas HTML** personalizadas
- 🔧 **Configuración basada en archivos .env** para máxima flexibilidad
- 📊 **Documentación automática con Swagger**
- 🛡️ **Validación robusta de datos de entrada**
- 🔄 **Respuestas HTTP estándar** para fácil integración
- 📝 **Logging integrado** para monitoreo y debugging

## 🛠️ Tecnologías

| Tecnología | Versión | Propósito |
|------------|---------|-----------|
| [.NET](https://dotnet.microsoft.com/) | 6.0+ | Framework principal |
| [ASP.NET Core](https://docs.microsoft.com/aspnet/core/) | 6.0+ | API REST Framework |
| [SendGrid](https://sendgrid.com/) | 9.29.3 | Servicio de email |
| [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) | 6.2.3 | Documentación API |
| [DotNetEnv](https://github.com/tonerdo/dotnet-env) | 3.0.0 | Gestión de variables de entorno |

## 📋 Prerrequisitos

Antes de comenzar, asegúrate de tener instalado:

- [.NET 6 SDK](https://dotnet.microsoft.com/download/dotnet/6.0) o superior
- Una cuenta activa en [SendGrid](https://sendgrid.com/)
- Un editor de código (recomendado: [Visual Studio Code](https://code.visualstudio.com/))

## 🚀 Instalación

### 1. Clonar el repositorio
```bash
git clone https://github.com/JhonierSerna14/MsNotifications.git
cd MsNotificaciones
```

### 2. Restaurar dependencias
```bash
dotnet restore
```

### 3. Configurar variables de entorno
```bash
# Copiar el archivo de ejemplo
cp .env.example .env
```

## ⚙️ Configuración

### Configuración de SendGrid

1. **Crear cuenta en SendGrid** (si no tienes una)
2. **Generar API Key**:
   - Ve a Settings → API Keys
   - Crea una nueva API Key con permisos de "Mail Send"
3. **Configurar plantilla de email** (opcional):
   - Ve a Email API → Dynamic Templates
   - Crea o usa una plantilla existente

### Archivo .env

Edita el archivo `.env` con tus credenciales:

```env
# Configuración de SendGrid
SENDGRID_API_KEY=SG.tu_api_key_real_aqui

# Configuración del remitente
FROM_EMAIL=eventos@tudominio.com
FROM_NAME=Sistema de Eventos

# ID de la plantilla de SendGrid
SENDGRID_TEMPLATE_ID=d-tu_template_id_aqui
```
## 🏃‍♂️ Uso

### Ejecutar en modo desarrollo
```bash
dotnet run
```

### Ejecutar en modo producción
```bash
dotnet run --configuration Release
```

### Acceder a la documentación
Una vez iniciado el servicio, puedes acceder a:

- **Swagger UI**: `https://localhost:7267/swagger`
- **API Base URL**: `https://localhost:7267`

## 📡 API Endpoints

### POST /Notification/ModificacionEmail

Envía una notificación de modificación de evento por email.

#### Request Body
```json
{
  "destinationEmail": "usuario@ejemplo.com",
  "destinationName": "Juan Pérez",
  "emailSubject": "Cambio en tu evento registrado",
  "newEventDate": "2024-01-15 18:00",
  "eventImageUrl": "https://ejemplo.com/imagen-evento.jpg",
  "eventUrl": "https://ejemplo.com/evento/123"
}
```

#### Parámetros

| Campo | Tipo | Requerido | Descripción |
|-------|------|-----------|-------------|
| `destinationEmail` | string | ✅ | Email del destinatario |
| `destinationName` | string | ✅ | Nombre del destinatario |
| `emailSubject` | string | ✅ | Asunto del email |
| `newEventDate` | string | ✅ | Nueva fecha del evento |
| `eventImageUrl` | string | ✅ | URL de la imagen del evento |
| `eventUrl` | string | ✅ | URL para acceder al evento |

#### Respuestas

| Código | Descripción | Ejemplo |
|--------|-------------|---------|
| `200 OK` | Email enviado exitosamente | `"Email sent successfully"` |
| `400 Bad Request` | Error en los datos o configuración | `"SendGrid API Key not configured"` |
| `400 Bad Request` | Error al enviar email | `"Error sending email"` |

#### Ejemplo con cURL
```bash
curl -X POST "https://localhost:7267/Notification/ModificacionEmail" \
  -H "Content-Type: application/json" \
  -d '{
    "destinationEmail": "test@ejemplo.com",
    "destinationName": "Juan Pérez",
    "emailSubject": "Evento Modificado",
    "newEventDate": "2024-01-15 18:00",
    "eventImageUrl": "https://ejemplo.com/imagen.jpg",
    "eventUrl": "https://ejemplo.com/evento"
  }'
```

## 📁 Estructura del Proyecto

```
MsNotificaciones/
├── Controllers/
│   └── NotificationController.cs    # Controlador principal de la API
├── Models/
│   └── EmailModel.cs               # Modelo de datos para emails
├── Properties/
│   └── launchSettings.json         # Configuración de desarrollo
├── .env                           # Variables de entorno (no versionado)
├── .env.example                   # Plantilla de variables de entorno
├── .gitignore                     # Archivos ignorados por Git
├── Program.cs                     # Punto de entrada de la aplicación
├── MsNotificaciones.csproj        # Configuración del proyecto
├── appsettings.json              # Configuración de la aplicación
├── appsettings.Development.json   # Configuración de desarrollo
└── README.md                     # Documentación del proyecto
```

## 🐛 Troubleshooting

### Problemas Comunes

**1. Error: "SendGrid API Key not configured"**
- Verifica que el archivo `.env` existe y contiene `SENDGRID_API_KEY`
- Asegúrate de que la API Key sea válida y tenga permisos de envío

**2. Error: "dotnet command not found"**
- Instala .NET 6 SDK desde el sitio oficial
- Verifica que `dotnet` esté en tu PATH

**3. Error 400 al enviar email**
- Verifica que todos los campos requeridos estén presentes
- Confirma que la plantilla de SendGrid existe y es válida

---

<div align="center">
  
**⭐ Si este proyecto te resulta útil, considera darle una estrella en GitHub ⭐**

</div>
