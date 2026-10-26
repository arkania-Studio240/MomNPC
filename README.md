# MomTotem 1.0.0

Plugin para Paper que permite que el NPC `mom` de FancyNpcs entregue **un único tótem por UUID de jugador**. Las reclamaciones se guardan en `plugins/MomTotem/config.yml` y sobreviven reinicios.

## Requisitos

- Servidor Paper con Java 21 y API compatible con Paper 1.21.4.
- FancyNpcs instalado.
- No requiere LuckPerms ni PlaceholderAPI.

> Como todavía no se confirmó la versión exacta del servidor, este proyecto está configurado para compilar contra Paper 1.21.4. Si tu servidor usa otra versión, conviene ajustar la dependencia de Paper antes de compilar.

## Instalar

1. Compila el proyecto para obtener `build/libs/MomTotem-1.0.0.jar`.
2. Sube ese JAR a la carpeta `plugins` desde el panel del hosting.
3. Reinicia el servidor (evita `/reload`).
4. Asegúrate de que FancyNpcs también esté instalado y funcionando.

## Conectar el NPC `mom`

Ejecuta en el juego como administrador o desde la consola:

```text
/npc action mom RIGHT_CLICK add console_command momtotem claim {player}
```

Si `mom` ya tiene una acción anterior que da un tótem directamente, elimina esa acción para que no entregue una segunda recompensa. Revisa las acciones con los comandos de ayuda de FancyNpcs de tu versión.

## Comportamiento

- Primer clic: registra el UUID y entrega exactamente un tótem.
- Clics posteriores: no entrega más tótems.
- Inventario lleno: no registra la reclamación; el jugador puede volver cuando tenga espacio.
- Consola guarda la reclamación en el archivo de configuración antes de entregar el objeto.
- Los comandos de reclamación están limitados a la consola, que es quien ejecuta la acción de FancyNpcs.

## Obtener el JAR usando GitHub Actions (sin instalar herramientas en tu PC)

1. Crea un repositorio nuevo en GitHub.
2. Sube todos los archivos de esta carpeta, incluida la carpeta `.github/workflows`.
3. Abre la pestaña **Actions** y ejecuta **Build MomTotem** (o espera a que termine el flujo automático).
4. En la ejecución completada, descarga el artefacto **MomTotem-jar**. Dentro estará `MomTotem-1.0.0.jar`.
5. Sube el JAR a `plugins/` en el panel y reinicia el servidor.

## Seguridad y límites

El plugin evita reclamaciones duplicadas mediante UUID, no mediante nombres ni permisos de LuckPerms. La integración se hace mediante la acción `console_command` de FancyNpcs; no necesita depender de la API interna de FancyNpcs.
