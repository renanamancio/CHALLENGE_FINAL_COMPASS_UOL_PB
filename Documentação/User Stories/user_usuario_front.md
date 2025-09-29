## 1. User Story: [Frontend] Fluxo de Reserva de Ingresso (Usuário Padrão)
## ID: US 04

### Como um **Usuário Registrado** da aplicação de cinema,
### Eu quero **navegar pelos filmes, visualizar as sessões disponíveis, selecionar assentos e concluir a compra**,
### Para que eu possa **comprar e gerenciar meus ingressos** através de uma interface intuitiva.

---

### Definição de Preparado (DoR - Definition of Ready)

A história é considerada pronta para começar se:

* **Integração de API:** Os serviços `api/auth.js`, `api/movies.js`, `api/sessions.js`, `api/reservations.js` estão criados e conectados à API backend.
* **Autenticação:** O `AuthContext` está implementado para gerenciar o estado de login e o armazenamento do JWT em `localStorage`.
* **Rotas:** Rotas principais (`/`, `/login`, `/movie/:id`, `/reservations`) estão configuradas via `React Router v6`.
* **Design Base:** Estilização base via `Styled Components` e a estrutura de componentes compartilhados (`Header/`, `Footer/`) estão prontos.

---

### Definição de Pronto (DoD - Definition of Done)

A história é considerada concluída se:

* **Fluxo de Reserva Completo:** É possível selecionar filme, sessão, assentos e **enviar a reserva** via `POST /reservations`.
* **Feedback Visual:** A interface exibe o estado de carregamento e mensagens de sucesso/erro (via `AlertContext`) após a tentativa de reserva.
* **Assentos:** A representação dos assentos na tela reflete a disponibilidade (livre/ocupado) obtida via API.
* **Gestão de Reservas:** A página de gerenciamento de reservas exibe as reservas do usuário logado (`GET /reservations/me`).
* **Segurança de Rota:** Rotas de compra e gerenciamento de reservas redirecionam o usuário **não autenticado** para a tela de login.

---

### Critérios de Aceite (Acceptance Criteria)

| # | Cenário | Ator | Quando | Então | Rotas/Serviços Envolvidos |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | **Navegação Detalhada** | Usuário (Qualquer) | Clica em um filme na Home | É direcionado para a página `MovieDetail/` e vê as sessões. | `GET /movies`, `GET /sessions` |
| **2** | **Seleção de Assentos** | Usuário Autenticado | Entra na tela de seleção de assentos para uma sessão | O sistema exibe o layout de assentos e permite a seleção. | `pages/SeatSelection` |
| **3** | **Compra Concluída** | Usuário Autenticado | Finaliza a seleção e clica em "Comprar" | A UI exibe a confirmação e redireciona para a lista de reservas. | `POST /reservations`, `api/reservations.js` |
| **4** | **Restrição de Login** | Usuário Não Autenticado | Tenta acessar a rota de "Reservar Ingresso" | O app é redirecionado para a página `Login/`. | `AuthContext.js`, `React Router v6` |
| **5** | **Visualização de Reservas** | Usuário Autenticado | Acessa a página de `Reservation Management` | O app exibe a lista das suas reservas ativas. | `GET /reservations/me` |