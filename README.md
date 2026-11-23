# Axioma · Taller de demostraciones

Axioma es una app web para practicar demostraciones matemáticas en formato de **tres columnas**: referencia, regla de inferencia y conclusión. Avanzas paso a paso, desde las premisas hasta la conclusión, con niveles de dificultad que van subiendo.

**Pruébala aquí:** https://carlosgbarradas.github.io/axioma/

---

## Qué puedes practicar

| Tema | Demostraciones |
|---|---|
| Silogismos (figuras 1–4 y por contradicción) | 17 |
| Números reales (axiomas de campo y orden) | 7 |
| Geometría (paralelismo en el plano) | 2 |
| Continuidad (definición ε–δ) | 3 |
| Derivadas (cociente incremental) | 2 |
| Ecuaciones diferenciales (verificación de soluciones) | 2 |

Cada demostración se practica en cuatro niveles:

1. **Opciones.** Elige la referencia, la regla o la conclusión que completa cada paso.
2. **Fichas.** Reconstruye la parte que falta ordenando fichas.
3. **Huecos.** Escribe la respuesta. Hay un teclado de símbolos (∀, ∃, ⇒, ε, δ…).
4. **Prueba completa.** Redacta tu propia tabla, o sube una foto de tu prueba en papel, y compárala con la demostración modelo.

## Talleres de razonamiento

- **¿Cómo empiezo?** Eliges una estrategia para atacar el enunciado y escribes la primera línea.
- **Encuentra el primer error.** Localizas el primer paso inválido de una demostración, explicas por qué falla y lo corriges.

## Seguimiento del avance

- Cada persona entra con su **correo y contraseña**, y su progreso se guarda en su cuenta.
- La sección **Mi progreso** muestra el avance por tema y por taller, y cómo resolviste cada paso: al primer intento, con reintento, con pista o viendo la respuesta.
- Los pasos en los que necesitaste ayuda quedan en una lista para **repasarlos** después.
- La sección **Referencias** reúne símbolos, reglas de inferencia, axiomas y ejemplos en Lean 4.

---

## Cómo funciona por dentro

Toda la app vive en un solo archivo, `index.html`, sin dependencias de compilación. El progreso se guarda así:

- **Modo en línea (Supabase).** Cada usuario tiene su cuenta y su avance se sincroniza en la nube, así que lo recupera desde cualquier dispositivo. Si se pierde la conexión, la app sigue guardando en el navegador y sube los cambios al reconectarse.
- **Modo local.** Si no hay claves de Supabase configuradas, el avance se guarda solo en el navegador, separado por correo.

### Activar el guardado en línea

1. Crea un proyecto gratis en [supabase.com](https://supabase.com).
2. En **SQL Editor**, ejecuta el script SQL que está en el comentario `GUARDADO EN LÍNEA`, al inicio del script de `index.html`. Crea la tabla `progress` con reglas (RLS) para que cada usuario solo pueda leer y escribir su propio progreso.
3. En **Authentication → Sign In / Providers → Email**, desactiva **Confirm email**.
4. En **Project Settings → API**, copia la *Project URL* y la clave *anon public*.
5. Pégalas en `index.html`:

   ```js
   const CLOUD={url:"https://TU-PROYECTO.supabase.co",anonKey:"TU_CLAVE_ANON"};
   ```

La clave *anon* está pensada para ir en el código del navegador: los datos los protegen las reglas RLS de la tabla.

> Por ahora no hay recuperación de contraseña, porque requiere configurar un servidor de correo (SMTP) en Supabase.

### Publicar cambios

Sube la nueva versión de `index.html` al repositorio (**Add file → Upload files → Commit changes**). GitHub Pages actualiza el sitio en uno o dos minutos y el progreso de los usuarios no se pierde.

---

Hecho por [@carlosgbarradas](https://github.com/carlosgbarradas).
