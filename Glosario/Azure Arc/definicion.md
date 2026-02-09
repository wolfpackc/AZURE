# -> Frase humana

> Azure Arc permite administrar servidores y servicios que están fuera de Azure desde el mismo panel y con las mismas reglas que si estuvieran dentro.

---

#  Problema real

Imagina una empresa que tiene:

* Servidores físicos en su oficina
* Máquinas virtuales en AWS
* Máquinas virtuales en Azure

Resultado:

Tres mundos separados.
Tres paneles distintos.
Tres formas de gestionar.

Eso es un caos.

---

#  Qué quiere resolver Azure Arc

> Permitir que **recursos que NO están en Azure** aparezcan y se gestionen **como si estuvieran en Azure**.

Nada más.

No los mueve a Azure.
No los convierte en Azure.
Solo los **registra** en Azure.

---

#  Idea simple

Azure Arc es como ponerle una **etiqueta de Azure** a cosas que están fuera.

---

# 🔹 Qué tipos de cosas puede registrar Azure Arc

* Servidores físicos
* VMs on-premise
* VMs en AWS
* VMs en Google Cloud
* Kubernetes

---

#  Qué haces técnicamente

En el servidor externo instalas un **agente de Azure Arc**.

Ese agente:

* Se autentica con tu tenant
* Se registra en Azure

Desde ese momento:

El servidor aparece en el Portal Azure.

---

#  Qué ves después

En el Portal Azure ves:

```
Servidor-Oficina-01
Servidor-AWS-02
VM-Azure-03
```

Todos juntos.

---

#  Qué puedes hacer con ellos

Desde Azure:

✅ Asignar políticas
✅ Ver inventario
✅ Aplicar parches
✅ Monitorizar
✅ Usar Defender
✅ Controlar permisos con RBAC

Aunque físicamente estén fuera.

---

# ❗ Qué NO hace Azure Arc

❌ No migra servidores
❌ No los ejecuta en Azure
❌ No paga cómputo

Siguen siendo tuyos.

---

# 🔐 Seguridad

Azure Arc:

* Usa Entra ID
* Usa certificados
* Usa canales cifrados

Es como si el servidor hiciera:

“Hola Azure, existo y soy este”.

---
✅ Sí

Les instalas el agente (no es solo una “etiqueta”, es un agente software).

Aparecen en el portal de Azure.

Puedes gestionarlas (políticas, monitorización, parches, seguridad, etc.).

❌ No

NO pueden usar Managed Identity (MSI) como los servicios nativos de Azure.

NO saltan las fronteras de tenant.

🔑 Punto clave

Azure Arc registra el servidor en TU tenant.

Una vez registrado:

➡️ Ese servidor pasa a pertenecer a tu tenant a efectos de identidad.

Pero:

No obtiene una Managed Identity automática como una VM nativa de Azure.

Para acceder a otros servicios se usan service principals, certificados o credenciales, no MSI.
