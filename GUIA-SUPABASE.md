# Guía: Configurar el sistema de carga de PDFs (Supabase)

El sistema de Reuniones usa **Supabase** (gratuito) para guardar los PDFs en la
nube. Así puedes subir reuniones cada semana desde la web, sin tocar código, y
quedan visibles para todos de forma permanente.

Sigue estos pasos **una sola vez** (~10 minutos).

---

## Paso 1 — Crear cuenta en Supabase

1. Entra a https://supabase.com
2. Haz clic en **Start your project** e inicia sesión con tu cuenta de GitHub.
3. Es gratis (plan Free: 1 GB de almacenamiento, suficiente para cientos de PDFs).

## Paso 2 — Crear un proyecto

1. Clic en **New project**.
2. Nombre: `jjc-reuniones` (o el que quieras).
3. Pon una contraseña de base de datos (guárdala, aunque no la usaremos aquí).
4. Región: elige **South America (São Paulo)** por cercanía.
5. Clic en **Create new project** y espera ~2 minutos a que se cree.

## Paso 3 — Crear el bucket de almacenamiento

1. En el menú lateral, entra a **Storage**.
2. Clic en **New bucket**.
3. Nombre exacto: `reuniones` (en minúsculas).
4. Activa la opción **Public bucket** (para que los PDFs se puedan ver).
5. Clic en **Create bucket**.

## Paso 4 — Permitir subir archivos (políticas)

1. Dentro de Storage, entra a la pestaña **Policies**.
2. En el bucket `reuniones`, clic en **New policy** → **For full customization**.
3. Crea una política que permita `INSERT` y `SELECT` para todos:
   - Policy name: `public-read-write`
   - Allowed operation: marca **SELECT** e **INSERT**
   - Target roles: `anon`
   - USING expression: `true`
   - WITH CHECK expression: `true`
4. Guarda.

> Nota de seguridad: esto permite que cualquiera con la página pueda subir.
> Para uso interno de tu equipo está bien. Si más adelante quieres restringir
> quién sube (con login), se puede agregar.

## Paso 5 — Copiar tus credenciales

1. En el menú lateral, entra a **Project Settings** (engranaje) → **API**.
2. Copia estos dos datos:
   - **Project URL** (algo como `https://xxxxx.supabase.co`)
   - **anon public** key (una clave larga)

## Paso 6 — Pegar las credenciales en index.html

1. Abre `index.html` y busca estas líneas (cerca del final, en el `<script>`):

   ```js
   const SUPABASE_URL = "TU_SUPABASE_URL";
   const SUPABASE_KEY = "TU_SUPABASE_ANON_KEY";
   ```

2. Reemplaza con tus datos reales:

   ```js
   const SUPABASE_URL = "https://xxxxx.supabase.co";
   const SUPABASE_KEY = "eyJhbGciOi....(tu clave anon)";
   ```

3. Guarda y sube el `index.html` a GitHub. Vercel se actualiza solo.

---

## ¡Listo! Cómo usar el sistema

- En la web, sección **Reuniones**, clic en **Subir PDF**.
- Elige **Mes**, **Semana (1–4)**, **Año**, un título opcional, y selecciona el PDF.
- Clic en **Subir a la nube**. El PDF aparece al instante en el mes correspondiente.
- Cualquier persona que entre a la web verá los PDFs organizados por mes y semana.

## Cómo se organizan los archivos

Los PDFs se guardan con este formato automático:
```
2026/07-semana-3-titulo.pdf
```
- `2026` = año
- `07` = mes (julio)
- `semana-3` = tercera semana
- El sistema los agrupa solos en el acordeón por mes.

## Límites del plan gratuito

- 1 GB de almacenamiento (un PDF pesa ~1-5 MB → caben cientos).
- Si algún día necesitas más, Supabase tiene planes de pago económicos.
