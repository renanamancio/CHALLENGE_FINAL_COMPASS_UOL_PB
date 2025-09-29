## 2. User Story: [Frontend] Acesso e Uso do Painel Administrativo
## ID: US 03

### Como um **Administrador** da aplicação de cinema,
### Eu quero **acessar o Dashboard de Administração** para gerenciar Filmes, Teatros, Sessões e todas as Reservas,
### Para que eu possa **manter o catálogo e a programação** do cinema atualizados de forma centralizada.

---

### Definição de Preparado (DoR - Definition of Ready)

A história é considerada pronta para começar se:

* **Backend Admin:** Os endpoints do backend que exigem privilégio de Administrador (`POST/PUT/DELETE /movies`, `GET /reservations` etc.) estão prontos para consumo.
* **Rotas Admin:** As rotas de administração (`/admin`, `/admin/movies`, `/admin/theaters`) estão definidas no `React Router v6`.
* **Contexto de Autenticação:** O `AuthContext` é capaz de determinar e armazenar se o usuário logado possui o **perfil de Administrador**.
* **API Admin:** Serviços de API (`movies.js`, `theaters.js`, etc.) possuem as funções necessárias para `POST`, `PUT` e `DELETE`.

---

### Definição de Pronto (DoD - Definition of Done)

A história é considerada concluída se:

* **Dashboard de Admin:** A estrutura básica da página `pages/Admin/` está implementada.
* **Proteção de Rota:** A rota `/admin` e sub-rotas **só são acessíveis** se o `AuthContext` confirmar que o usuário é um Administrador.
* **CRUD de Conteúdo (UI):** As interfaces para **Criação, Edição e Exclusão** de Filmes e Teatros estão funcionais e comunicam-se com a API.
* **Gerenciamento de Reservas (UI):** A interface lista **todas** as reservas do sistema e permite ao Admin visualizar e **atualizar o status** de uma reserva específica.
* **Feedback de Erro:** Erros de permissão (ex: 403) ou falhas de comunicação da API são tratados e exibidos na tela.

---

### Critérios de Aceite (Acceptance Criteria)

| # | Cenário | Ator | Quando | Então | Rotas/Serviços Envolvidos |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | **Acesso ao Dashboard** | Administrador Autenticado | Acessa a rota `/admin` | O sistema exibe o painel de administração com as opções de gestão. | `pages/Admin/` |
| **2** | **Restrição de Acesso** | Usuário Padrão Autenticado | Tenta acessar a rota `/admin` | O sistema **redireciona** para a página inicial (ou exibe erro 403 na UI). | `AuthContext.js`, Rota Protegida |
| **3** | **Criação de Filme (UI)** | Administrador | Preenche e envia o formulário de `Criar Filme` | A tela exibe mensagem de sucesso e o novo filme aparece na lista. | `POST /movies`, `pages/Admin/` |
| **4** | **Exclusão de Teatro (UI)** | Administrador | Clica em "Excluir" em um item de Teatro | O app solicita confirmação e, se confirmado, envia o `DELETE` e atualiza a lista. | `DELETE /theaters`, `api/theaters.js` |
| **5** | **Gestão Total de Reservas** | Administrador | Acessa a lista de reservas | A tela exibe uma tabela com **todas** as reservas, não apenas as suas, permitindo a edição de status. | `GET /reservations` |