# TEST-CASE: [NN-slug] — [Nome da Funcionalidade]

> **Use Case:** `[UC-NN]` | **User Story:** `[US-NN]` | **Status:** `Draft` *(Draft | Em revisão | Aprovado)*  
> **Versão:** 1.0 | **Data:** YYYY-MM-DD | **Glossário/ADRs:** `[GLOSSARIO.md]`, `[ADR-NNN]`

> O domínio "checkout" abaixo é só ilustração da forma. Não copiar para um pacote real. Os IDs seguem `TC-NN.MM`.

---

## 1. Seams (Fronteiras Públicas de Teste)

> Testes validam comportamento apenas nas interfaces públicas abaixo. Confirmar antes do `Execute`.

| ID | Seam (Interface Pública) | O que captura | O que deixa passar |
| :--- | :--- | :--- | :--- |
| `SEAM-01` | Ex: `POST /api/v1/checkout` | Contrato HTTP, auth, status codes e fluxo completo. | UI/frontend e latência real de terceiros. |
| `SEAM-02` | Ex: `CheckoutService.execute()` | Regras de negócio, cálculos e invariantes de domínio. | Roteamento HTTP e serialização JSON. |

---

## 2. Massa de Dados Base (Fixtures)

> Valores literais fixos usados como fonte de verdade independente (zero tautologia).

* **`USER_VALID`:** `{ id: "u-01", role: "CUSTOMER", active: true }`
* **`CART_VALID`:** `{ items: [{ sku: "A1", qty: 2, unitPrice: 50.00 }], coupon: "DESC10" }` *(total esperado: `90.00`)*
* **`CART_EMPTY`:** `{ items: [] }`

---

## 3. Cenários de Teste (Ordem de Fatias Verticais)

> Executar em **fatias verticais** (1 teste → 1 implementação mínima → repetir), na ordem abaixo.

### `TC-{{NN}}.01` — [Caminho Feliz] Usuário finaliza compra com carrinho válido
* **Seam:** `SEAM-02` | **Rastreabilidade:** `CA-01`, `RU-{{NN}}.1`
* **Dado** `USER_VALID` autenticado com `CART_VALID` (2 itens de `50.00` + cupom `DESC10`);
* **Quando** acionar a finalização da compra;
* **Então** retorna pedido `CONFIRMED` com `subtotal: 100.00`, `discount: 10.00` e `total: 90.00`.

### `TC-{{NN}}.02` — [Exceção] Rejeita compra com carrinho vazio
* **Seam:** `SEAM-02` | **Rastreabilidade:** `CA-02`, `RU-{{NN}}.2`
* **Dado** `USER_VALID` com `CART_EMPTY`;
* **Quando** tentar finalizar a compra;
* **Então** falha com erro de domínio `EMPTY_CART` (HTTP `422` na `SEAM-01`) e nenhum pedido é criado.

### `TC-{{NN}}.03` — [Caso de Borda] Desconto maior que subtotal limita total a zero
* **Seam:** `SEAM-02` | **Rastreabilidade:** `RU-{{NN}}.3`
* **Dado** carrinho com `subtotal: 100.00` e desconto fixo de `150.00`;
* **Quando** finalizar a compra;
* **Então** o `total` calculado deve ser exatamente `0.00`.

### `TC-{{NN}}.04` — [Segurança] Bloqueia requisição sem autenticação válida
* **Seam:** `SEAM-01` | **Rastreabilidade:** `CA-04`
* **Dado** requisição sem token Bearer válido;
* **Quando** chamar `POST /api/v1/checkout`;
* **Então** retorna HTTP `401 Unauthorized`.

---

## 4. Checklist de Aprovação (DoR)

- [ ] Todos os Critérios de Aceite da `USER-STORY` e fluxos do `USE-CASE` estão cobertos.
- [ ] Todas as *seams* estão claras (o que capturam / deixam passar) e aprovadas.
- [ ] Nenhum teste acopla a detalhes internos (métodos privados, SQL direto ou mocks internos).
- [ ] Todos os resultados esperados usam valores literais independentes e seguem o `GLOSSARIO.md`.
