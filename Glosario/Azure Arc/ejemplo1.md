

---

### 🏢🏢🏢🏢🏢🏢 Empresa: *FábricaTech S.L.🏢🏢🏢🏢🏢🏢🏢🏢*

Tiene:

* 10 servidores en su oficina (on-premise)
* 5 máquinas virtuales en Azure

---

## 🔹 Caso 1: VM dentro de Azure

Una VM en Azure necesita leer secretos de **Azure Key Vault**.

👉 Le activan **Managed Identity**
👉 En Key Vault dan permiso a esa identidad
👉 La VM accede **sin usuario ni contraseña**

✅ Automático
✅ Seguro
✅ Sin claves

---

## 🔹 Caso 2: Servidor físico en oficina con Azure Arc

Instalan **Azure Arc agent** en el servidor.

Ahora:

* Aparece en el portal de Azure
* Microsoft puede aplicar políticas
* Monitorización centralizada

Pero…

Si ese servidor quiere leer Key Vault:

👉 NO puede usar Managed Identity
👉 Deben crear un **Service Principal**
👉 Guardar certificado o secreto

❌ Ya hay credenciales
❌ Más gestión

---

## 🔹 Caso 3: Servidor sin Azure Arc

* No aparece en Azure
* No se le aplican políticas
* No hay control centralizado

Todo se gestiona localmente.

---

##  Resumen rápido

| Tipo de máquina | ¿Aparece en Azure? | ¿Puede usar MSI? |
| --------------- | ------------------ | ---------------- |
| VM Azure        | Sí                 | Sí               |
| On-prem con Arc | Sí                 | No               |
| On-prem sin Arc | No                 | No               |

---

### 🧠 Idea clave

Azure Arc **no convierte** servidores externos en servidores Azure.
Solo los **hace visibles y gestionables**.
