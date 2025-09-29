## 1. User Story: Reserva de Assentos (Usuário Padrão)
## ID: US 02

### Como um **Usuário do sistema (Padrão)**,
### Eu quero **selecionar um filme, escolher uma sessão e reservar assentos**,
### Para que eu possa **garantir meu ingresso de cinema de forma rápida e segura**.

---

### Definição de Preparado (DoR - Definition of Ready)

A história é considerada pronta para começar se:

* **Autenticação:** Os endpoints de registro e login (`/auth/register`, `/auth/auth/login`) estão implementados e funcionais.
* **Conteúdo:** Modelos (schemas) e endpoints de listagem de Filmes e Sessões (`GET /movies`, `GET /sessions`) estão finalizados.
* **Infraestrutura:** Conexão com MongoDB e Mongoose configurada.
* **Segurança:** Mecanismo de JWT para autenticação do usuário implementado.

---

### Definição de Pronto (DoD - Definition of Done)

A história é considerada concluída se:

* **CRUD de Reserva (Criação/Listagem Própria):** O endpoint `POST /api/v1/reservations` está implementado para criar uma nova reserva.
* **Listagem:** O endpoint `GET /api/v1/reservations/me` está implementado para listar as reservas do usuário logado.
* **Regra de Negócio (Assento):** A lógica impede a reserva de assentos que já estão ocupados na sessão.
* **Segurança:** As rotas estão protegidas e requerem autenticação (JWT).
* **Testes:** Cobertura de testes de unidade e integração para o fluxo de reserva, incluindo cenários de sucesso e falha (assento ocupado, falta de autenticação).

---

### Critérios de Aceite (Acceptance Criteria)

| # | Cenário | Ator | Quando | Então | Endpoints |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | **Criação de Reserva** | Usuário Autenticado | Envio `POST` para criar reserva com assentos disponíveis. | Retorna status **201 Created** e a reserva é registrada. | `POST /api/v1/reservations` |
| **2** | **Reserva Própria** | Usuário Autenticado | Solicito `GET /api/v1/reservations/me`. | Retorna apenas as reservas feitas por este usuário. | `GET /api/v1/reservations/me` |
| **3** | **Assento Ocupado** | Usuário Autenticado | Tenta reservar assento que já consta como reservado na sessão. | Retorna erro **400 Bad Request** ou similar, com mensagem de indisponibilidade. | `POST /api/v1/reservations` |
| **4** | **Autenticação Obrigatória** | Usuário NÃO Autenticado | Tenta enviar `POST` para criar reserva. | Retorna erro **401 Não Autorizado**. | `POST /api/v1/reservations` |