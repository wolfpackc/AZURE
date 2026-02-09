## Diferencia

**Entra ID = quién eres**

**RBAC = qué puedes hacer**

---

## 🔹 Microsoft Entra ID → *Quién eres*

Aquí se gestionan:

* Usuarios
* Grupos
* Dispositivos
* Identidades administradas

Y cosas como:

* Contraseña
* MFA
* Si la cuenta existe o no
* A qué grupos pertenece
  
 Entra ID define **identidad**.

---

## 🔹 Azure RBAC → *Qué puedes hacer*

RBAC (Role-Based Access Control) define:

* Qué acciones puede hacer una identidad
* Sobre qué recursos
* En qué nivel (suscripción, resource group, recurso)

Ejemplos de roles:

* Owner
* Contributor
* Reader
* Virtual Machine Contributor

 RBAC define **permisos**.

---

## 🔹 Cómo trabajan juntos

1. Creas usuario en Entra ID
2. Le asignas un rol RBAC sobre un recurso

Ejemplo:

* Usuario: Juan
* Recurso: Suscripción Producción
* Rol: Reader

Resultado:

Juan puede **ver** recursos, pero no modificarlos.

---

## 🔹 Dispositivos y servicios

* Una VM con Managed Identity es una identidad en Entra ID
* A esa identidad también le asignas roles RBAC

Funciona igual que un usuario.

---

