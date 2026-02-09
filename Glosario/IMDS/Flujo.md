# 1️⃣ IMDS: un servicio interno en cada VM

Sí, **todas las máquinas virtuales de Azure (VMs, App Services, Functions) tienen acceso a IMDS**, que es **Instance Metadata Service**.

* No es algo externo, no sale a Internet.
* No hay que instalar nada, viene “por defecto” en la VM.
* Su función principal es **proporcionar metadatos de la VM y tokens de Managed Identity**.

Piensa en IMDS como un **portero interno**:

* Solo responde dentro de la VM
* Solo da información que esa VM puede ver
* Nunca sale a la red pública

---

# 2️⃣ La famosa IP 169.254.169.254

* Es una **IP especial reservada para servicios internos** (link-local)
* No es accesible desde fuera de la VM
* Cada VM sabe que para hablar con IMDS, tiene que “llamar a esa IP”

Es como decir:

> “Oye portero, soy yo dentro de la casa, ¿me das mi pase temporal?”

Todo esto sucede **solo dentro de tu VM**, la red externa no ve nada.

---

# 3️⃣ Flujo de solicitud de token (paso a paso)

Imagina que tienes una VM con una app que quiere acceder a un Storage o Key Vault:

1. **App dentro de la VM** hace una llamada HTTP a:

```
http://169.254.169.254/metadata/identity/oauth2/token
```

* Incluye headers que indican que quiere JSON y qué recurso necesita (Storage, Key Vault…).

2. **IMDS recibe la solicitud**

* Sabe qué VM es
* Sabe qué identidad (MSI) tiene asociada

3. **IMDS solicita un token a Azure AD (Entra ID)**

* Azure AD firma un token JWT para esa identidad, con permisos limitados y expiración corta

4. **IMDS devuelve el token a la app**

5. **App usa el token** para llamar a Storage, Key Vault, Cosmos DB…

* El servicio verifica la firma del token con la **clave pública de Microsoft**
* Si es válido → acceso concedido

---

# 4️⃣ Importante: todo ocurre **internamente**

* El token nunca sale por error a Internet
* No hay contraseña ni secreto guardado en archivos
* El endpoint 169.254.169.254 **solo escucha dentro de la VM**, nadie más puede usarlo

---

# 5️⃣ Analogía mental

* **La VM** = casa
* **IMDS (169.254.169.254)** = portero dentro de la casa
* **Token** = pase temporal que el portero te da
* **Servicio Azure (Storage, Key Vault…)** = discoteca donde necesitas el pase

La app solo “pide al portero dentro de la casa” y obtiene el pase.

---

# 6️⃣ Frase corta para memorizar

> IMDS es un servicio interno de la VM que te da tokens temporales.
> La IP 169.254.169.254 solo existe dentro de la VM.
