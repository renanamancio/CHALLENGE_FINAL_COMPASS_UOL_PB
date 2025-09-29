## User Story: Gerenciamento de Sistema (Administrador)
## ID: US 01

### Como um **Administrador do sistema**,
### Eu quero **gerenciar o CRUD completo de Filmes, Teatros, Sessões, e todas as Reservas**,
### Para que eu possa **manter o sistema operacional, atualizado e prestar suporte ao cliente**.

---

### Definição de Preparado (DoR - Definition of Ready)

A história é considerada pronta para começar se:

* **US 1 Concluída:** A User Story de Reserva (Usuário Padrão) está finalizada e testada.
* **Autorização:** A lógica de segurança para verificar o **perfil de Administrador** está implementada em um middleware.
* **Modelos:** Todos os modelos (Filmes, Teatros, Sessões, Reservas) estão definidos no MongoDB.
* **Dados de Teste:** Scripts de *seed* (população inicial) estão disponíveis para o ambiente de testes.

---

### Definição de Pronto (DoD - Definition of Done)

A história é considerada concluída se:

* **CRUD de Gestão Completo:** Todos os endpoints para `Filmes`, `Teatros` e `Sessões` (`POST`, `PUT`, `DELETE`) estão implementados e protegidos por autorização (Admin).
* **Gerenciamento de Reservas:** Os endpoints `GET /api/v1/reservations` (todas), `PUT /api/v1/reservations/:id` (status), e `DELETE /api/v1/reservations/:id` estão implementados e protegidos (Admin).
* **Segurança (Perfis):** Testes de integração confirmam que **apenas o Administrador** pode acessar as rotas de gerenciamento (`POST/PUT/DELETE` em todos os recursos, e `GET/PUT/DELETE` em todas as reservas).
* **Usuário Padrão Restrito:** Testes confirmam que o Usuário Padrão recebe **403 Proibido** ao tentar acessar rotas exclusivas do Administrador.
* **Documentação:** A documentação da API foi atualizada, especificando claramente a restrição "somente administrador" para as rotas de gestão.

---

### Critérios de Aceite (Acceptance Criteria)

| # | Cenário | Ator | Quando | Então | Endpoints |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | **Gestão de Sessão** | Administrador | Envia `POST` para `/api/v1/sessions` (criar nova sessão). | Retorna status **201 Created** e a sessão é registrada. | `POST /api/v1/sessions` |
| **2** | **Acesso Total a Reservas** | Administrador | Solicita `GET /api/v1/reservations`. | Retorna **todas** as reservas do sistema. | `GET /api/v1/reservations` |
| **3** | **Restrição de Acesso (Padrão)** | Usuário Padrão | Tenta enviar `PUT` para `/api/v1/movies/:id` (editar filme). | Retorna erro **403 Proibido**. | `PUT /api/v1/movies/:id` |
| **4** | **Atualização de Status** | Administrador | Envia `PUT` para `/api/v1/reservations/:id` para alterar o status. | Retorna status **200 OK** e o status da reserva é alterado (ex: Cancelado). | `PUT /api/v1/reservations/:id` |
| **5** | **Exclusão de Usuário** | Administrador | Envia `DELETE` para `/api/v1/users/:id`. | Retorna status **200 OK** (ou 204) e o usuário é excluído do sistema. | `DELETE /api/v1/users/:id` |