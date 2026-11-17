AUTOMATIZACIÓN EN N8N PARA PEDIDOS DE CLIENTES

Agente conversacional para la gestión de pedidos de un taller multiservicio, construido en n8n con modelos Claude (Anthropic). Aplica principios de gobierno del dato en cada paso: seguridad, privacidad, minimización, mínimo privilegio y trazabilidad.

Workflow

💬 Qué puede hacer

Consultar un pedido por su ID → "Dime los datos del pedido P003"
Actualizar el estado de un pedido → "Pon el pedido P001 en curso"
Crear un pedido nuevo → "Crea el pedido P006 para X persona, teléfono XXXXXXXXX: cambio de tapas, XX €, Pendiente"

⚙️ Cómo funciona

Paso	Nodo	Qué hace	Principio de gobierno

1	Guardrails (Claude Haiku)	Bloquea jailbreaks, datos personales sensibles en la entrada (tarjeta, email, IBAN, DNI/NIE) y temas fuera del negocio	Seguridad y privacidad
2	AI Agent (Claude Sonnet) + system prompt	Aplica una política de datos escrita: no inventa datos, consulta solo por ID, no borra registros ni exporta listados	Control blando
3	Consultar pedidos	Solo por ID, un pedido cada vez	Minimización de datos por diseño
4	Actualizar estado	Solo puede modificar la columna estado (Pendiente, En curso, Listo)	Mínimo privilegio
5	Crear pedido	Exige todos los datos, comprueba antes que el ID no exista y clasifica la fila como Confidencial	Calidad e integridad del dato
6	Registro auditoría	Guarda fecha, sesión, pregunta, herramientas usadas y respuesta	Trazabilidad

Decisión de diseño — teléfono del cliente: el taller necesita el teléfono para avisar al cliente, así que se permite registrarlo y consultarlo. A cambio, cada fila se etiqueta con la clasificación Confidencial y todo acceso queda en el registro de auditoría.

⚠️ Todos los datos de ejemplo son ficticios. El workflow no incluye credenciales ni datos reales.
