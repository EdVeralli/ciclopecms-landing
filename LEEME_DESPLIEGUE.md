# ¿Cómo se publica este sitio?

**Este repo es la FUENTE DE VERDAD de `ciclopecms.com`, pero NO lo publica.**

El sitio lo sirve **Nginx desde el VPS** (`2.25.145.154`), donde `/var/www/ciclopecms` es un
**clon de git de este repo**.

## Para publicar un cambio

```bash
# 1) acá: editar, commitear y pushear a main
git push origin main

# 2) en el server:
ssh root@2.25.145.154
git -C /var/www/ciclopecms pull origin main
```

Nginx sirve los archivos al instante. No hay build, no hay CI, no hay que esperar nada.

⚠️ **Nunca copiar archivos a mano a `/var/www/ciclopecms`** — es un clon de git y el próximo `pull` choca.

## GitHub Pages: APAGADO (12-jul-2026)

Este repo **usaba** GitHub Pages hasta el 17-jun-2026. Después la home se migró al VPS (el DNS `@` de
`ciclopecms.com` pasó a apuntar a `2.25.145.154`), pero Pages quedó encendido y el archivo `CNAME`
redirigía `edveralli.github.io/ciclopecms-landing` → `ciclopecms.com`. Inofensivo, pero confuso: había
**dos mecanismos de publicación**, uno dormido.

El 12-jul-2026 se **apagó Pages y se borró el `CNAME`**. Ahora hay una sola forma de que algo de este
repo llegue a internet: el `git pull` en el VPS.

> Contexto: el 12-jul un asistente publicó el SLA nuevo pusheando acá y dando por hecho que Pages lo
> subía solo. No pasó nada (Pages ya no publicaba), pero el sitio quedó sin actualizar hasta que se
> corrió el `pull` en el server. Este archivo existe para que no vuelva a pasar.

## Dónde vive el resto

| | |
|---|---|
| `ciclopecms.com` | **este repo** → clonado en `/var/www/ciclopecms` (VPS, Nginx estático) |
| `demo.ciclopecms.com` (CMS Legal) | repo `EdVeralli/Ciclope-CMS-DIAN` → Docker en `/opt/ciclope` |
| `saas.ciclopecms.com` (CMS SaaS) | mismo repo y mismo stack |
