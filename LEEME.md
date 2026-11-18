# Aliado – guía para publicarlo (de cero a tu propio enlace)

Con esto tendrás **tu propia web/app**, con su dirección propia, que se abre directo en el navegador del celular
y se puede instalar con su icono. Ya no depende de claude.ai.

## Qué contiene
- `public/` → la app (pantalla, voz, carpetas, archivos). Es una PWA: se instala como app.
- `api/chat.js` → el "cerebro": recibe lo que dices, llama a Claude con **tu** clave y devuelve la respuesta.
  Tu clave vive solo en el servidor; nunca llega al celular de nadie.
- `.env.example` → los nombres de las variables secretas que debes crear en el hosting.

## Cuánto tiempo toma
Entre 30 y 60 minutos la primera vez, sin programar.

---

## Paso 1 · Cuentas que necesitas (las tres se abren desde el navegador)
1. **GitHub** (guarda tu código).
2. **Vercel** (publica la página y el servidor; puedes entrar con tu cuenta de GitHub).
   Revisa en su página de precios las condiciones del plan gratuito: algunos planes gratis están pensados
   para uso personal y no comercial. Para cobrar a clientes probablemente necesites un plan de pago.
3. **Claude Console** (para la API): crea una cuenta, genera una **API key** y compra algunos créditos.
   La API se paga aparte de cualquier suscripción de Claude.

## Paso 2 · Pon un límite de gasto (¡hazlo antes de publicar!)
En la Claude Console, entra a **Billing → Spend limits** y fija un tope mensual bajo (por ejemplo, el equivalente a
unos 10 dólares) mientras pruebas. Así, pase lo que pase, no te cobran de más.

## Paso 3 · Sube el proyecto a GitHub
1. En GitHub: **New repository** → nombre `aliado` → Create.
2. Descomprime este ZIP en tu computadora. En el repositorio pulsa **Add file → Upload files** y arrastra
   **todo el contenido** de la carpeta (`public`, `api`, `package.json`, `vercel.json`…). **Commit changes**.
   (No subas nunca un archivo `.env` con tu clave.)

## Paso 4 · Publica en Vercel
1. En Vercel: **Add New → Project** → elige tu repositorio `aliado` → Import.
2. En **Framework Preset** deja "Other". No cambies nada más.
3. Abre **Environment Variables** y crea:
   - `ANTHROPIC_API_KEY` = tu clave de la Claude Console.
   - `ACCESS_CODES` = códigos de acceso separados por coma, por ejemplo `PRUEBA-ANA,PRUEBA-LUIS,PRUEBA-MARIA`.
     Cada persona de prueba recibe **su propio código**. Si alguien abusa, lo quitas de la lista y listo.
4. Pulsa **Deploy**. En un minuto te da un enlace tipo `aliado-xxxx.vercel.app`. Ese es tu app.

## Paso 5 · Pruébala
1. Abre el enlace en el celular (mejor en **Chrome, Android**).
2. Toca ⚙️ → escribe tu **código de acceso** → Listo.
3. Toca 🎤 y di: "gasté 18 soles en almuerzo". Debe responderte con voz y aparecer en la carpeta Finanzas.
4. Prueba: "recuérdame entregar la monografía mañana, código rojo". Debe salir la alerta roja.
5. Adjunta un Word o Excel en una carpeta y pulsa "Abrir".
- **iPhone:** el dictado por voz de Safari es menos fiable. Si falla, usa el micrófono del teclado.

## Paso 6 · Instálala como app
- **Android (Chrome):** ⚙️ → "Instalar Aliado", o menú ⋮ → "Instalar app".
- **iPhone (Safari):** Compartir → "Añadir a pantalla de inicio".

## Paso 7 · Dirección propia (opcional, da confianza)
Compra un dominio (por ejemplo `tuaplicacion.com`) en cualquier proveedor y, en Vercel, ve a
**Settings → Domains** y sigue las instrucciones.

---

## Cuidado con el costo
Cada mensaje que le hablas a Aliado consume créditos de tu cuenta de la API. El modelo por defecto es el más
económico (`claude-haiku-5-5`). Controla el gasto con:
- el **límite de gasto** del Paso 2,
- los **códigos de acceso** (solo entra quien tú invitas),
- la variable `MAX_MSGS_10MIN` (límite de mensajes por persona cada 10 minutos).

## Antes de abrirlo al público y cobrar
Esta versión es ideal para **probar con 5–20 personas**. Para venderla a cualquiera faltan:
1. **Cuentas de usuario y nube.** Hoy cada persona guarda sus datos solo en su dispositivo. Para sincronizar entre
   celular y computadora y no perder datos hay que agregar inicio de sesión y una base de datos
   (por ejemplo Supabase o Firebase).
2. **Cobros.** Suscripción mensual con una pasarela de pagos disponible en Perú (por ejemplo Culqi, Mercado Pago,
   Stripe) o Yape/Plin manual al inicio. Calcula tu precio con el costo real por usuario.
3. **Legal.** Política de privacidad y términos de uso. En Perú aplica la Ley de Protección de Datos Personales
   (Ley 29733): consulta con un abogado o contador antes de recoger datos de terceros.
4. **Tienda de apps (opcional).** Una PWA se puede empaquetar para Google Play (por ejemplo con PWABuilder);
   Google cobra una cuota de desarrollador (revisa el monto vigente).
5. **Mejoras ya pensadas:** leer el contenido de tus Word/Excel/PowerPoint, plantillas de Gym y Clases,
   cierre del día, tareas repetidas y notificaciones.

## Si algo falla
- "Necesito tu código de acceso" → revisa ⚙️ y que el código esté en `ACCESS_CODES` (sin espacios).
- Responde "Lo guardé como nota…" → la IA no respondió: revisa `ANTHROPIC_API_KEY`, que tengas créditos,
  y en Vercel mira **Logs** del proyecto.
- Después de cambiar una variable en Vercel, haz **Redeploy** para que se aplique.
