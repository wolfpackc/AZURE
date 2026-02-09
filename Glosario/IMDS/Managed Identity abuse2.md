
#  Escenario típico MAL configurado

Tienes:

* Una Web App en Azure
* Usa Managed Identity
* La Web App necesita solo leer un secreto de Key Vault para conectarse a su base de datos

Pero el administrador hace esto:

 Asigna a la Managed Identity de la Web App el rol:

```
Contributor en la suscripción
```

---

## ❌ Qué significa esto

Esa identidad puede:

* Crear VMs
* Borrar recursos
* Leer secretos
* Modificar redes
* Acceder a casi todo

Muchísimo más de lo que necesita.

---

## ⚠️ Qué pasa si comprometen la Web App

Supón que hay una inyección de comandos y el atacante entra.

El atacante:

1. Pide token vía IMDS
2. Obtiene token de la identidad
3. Usa el token contra Azure Management API

Ahora puede:

* Crear nuevas VMs
* Añadir puertas traseras
* Robar configuraciones
* Borrar recursos

Todo porque la identidad tenía permisos excesivos.

---

#  Escenario CORRECTO

La Web App solo necesita:

* Leer 1 secreto de Key Vault

Entonces hacemos:

---

##  Paso 1: Identidad con mínimo privilegio

A la Managed Identity de la Web App le asignas:

```
Key Vault Secrets User
```

Solo sobre ESE Key Vault concreto.

Nada más.

---

##  Paso 2: Sin permisos de Azure Management

No:

* Contributor
* Owner
* Reader en suscripción

Cero permisos a nivel suscripción.

---

##  Paso 3: Identidades separadas

Si tienes:

* Web App
* Worker
* Admin script

Cada uno con su propia identidad.

No reutilizar la misma MSI.

---

#  Resultado si ahora comprometen la Web App

El atacante:

1. Pide token
2. Obtiene token
3. Intenta usarlo contra Azure Management

Resultado:

❌ Acceso denegado

Solo podría:

* Leer ese secreto concreto del Key Vault

Y ya.

No puede crear VMs.
No puede moverse lateralmente.

---

#  Tabla comparativa

| Caso                | Impacto si comprometen |
| ------------------- | ---------------------- |
| MSI con Contributor | Desastre               |
| MSI solo KeyVault   | Impacto mínimo         |

---

#  Regla de oro

> Cada identidad solo puede hacer exactamente lo que su aplicación necesita.

Ni más.
Ni menos.

---

#  Frase para memorizar

> Managed Identity no es peligrosa.
> Peligroso es dar demasiados permisos.

