# Integração Postman + GitHub

Repositório criado para testar e padronizar o **versionamento de collections do Postman via GitHub**, permitindo que o time acompanhe a evolução dos cenários de API de forma controlada, com histórico e rastreabilidade.

> Este repositório está conectado ao Postman através da integração **“Backup a collection”**, que salva automaticamente a collection oficial em um arquivo JSON sempre que ela é atualizada.

---

## 🎯 Objetivo

- Manter as **collections oficiais do Postman** versionadas em Git.
- Padronizar o **ponto de referência** para testes de API entre todos do time.
- Permitir **auditoria e histórico** de mudanças (quem alterou, quando, o que mudou).
- Servir como **modelo** para futuras integrações de outras APIs/teams.

---

## 📁 Estrutura do repositório

Estrutura atual (pode ser expandida no futuro):

```text
Integra-o-Postman-Git/
├── Postman Collections/
│   └── TestApi-GitHub.postman_collection.json   # Collection oficial da TestApi (backup automático do Postman)
├── TestApi-+ GITHUB.postman_collection.json     # Arquivo de teste inicial (pode ser descontinuado no futuro)
└── README.md
```

**Pasta principal utilizada pela integração:**

- `Postman Collections/`  
  Onde o Postman grava automaticamente os arquivos `.postman_collection.json` conectados via **Backup a collection**.

---

## 🔗 Como funciona a integração Postman → GitHub

A collection oficial **`TestApi + GITHUB`** está configurada no Postman com a integração:

- **Tipo:** `Backup a collection`
- **Repositório:** `KauePastori/Integra-o-Postman-Git`
- **Branch:** `main`
- **Diretório no repositório:** `Postman Collections/`
- **Arquivo:** `TestApi-GitHub.postman_collection.json`

Sempre que alguém:

1. Abre a collection oficial no Postman;
2. Faz alterações (requests, tests, scripts etc.);
3. E **salva** a collection;

➡️ o Postman envia automaticamente um novo backup para este repositório, atualizando o JSON correspondente.

Não é necessário fazer `git push` manual a partir do Postman: a integração cuida disso.

---

## 👩‍💻 Como o time deve atualizar a collection oficial

### 1. Pré-requisitos

- Ter acesso à **workspace** do Postman onde está a collection `TestApi + GITHUB`.
- Utilizar sempre a collection oficial (evitar trabalhar em cópias locais desconectadas).

### 2. Passo a passo (Postman → GitHub)

1. Abrir o **Postman** e acessar a workspace do time.
2. Localizar a collection **`TestApi + GITHUB`**.
3. Realizar as alterações necessárias:
   - adicionar/editar requests;
   - ajustar headers, bodies, params;
   - criar/editar scripts de teste etc.
4. Clicar em **Save** na collection (ou salvar os requests alterados).

Após o save, o Postman irá, em segundo plano, atualizar o arquivo:

```text
Postman Collections/TestApi-GitHub.postman_collection.json
```

no repositório `KauePastori/Integra-o-Postman-Git` na branch `main`.

---

## 🔍 Como visualizar as mudanças no GitHub

1. Acessar o repositório no GitHub.
2. Navegar até a pasta **`Postman Collections/`**.
3. Abrir o arquivo **`TestApi-GitHub.postman_collection.json`**.
4. Clicar em **History** / **Commits** para ver o histórico.
5. Abrir o commit desejado para visualizar o **diff** do JSON (requests novos, alterações de URL, métodos, bodies, testes etc.).

---

## ♻️ Recuperando a collection a partir do GitHub (se necessário)

Caso seja preciso restaurar uma versão específica da collection a partir do GitHub:

1. Baixar a versão desejada do arquivo `TestApi-GitHub.postman_collection.json` (via *Download raw* ou clone/pull).
2. No Postman, clicar em **Import → File**.
3. Selecionar o JSON baixado.
4. Escolher entre:
   - **Replace**: substituir a collection atual pela versão importada; ou
   - **Create a copy**: criar uma cópia para comparação antes de aplicar alterações na collection oficial.

---

## ✅ Boas práticas

- Tratar `TestApi + GITHUB` como a **collection oficial** de referência para a API.
- Evitar criar e manter cópias paralelas da mesma collection fora da workspace oficial.
- Não armazenar **segredos sensíveis** (tokens de produção, senhas etc.) em environments que sejam versionados em Git.
- Salvar a collection sempre que realizar alterações relevantes, garantindo que o backup esteja atualizado.
- Utilizar o histórico de commits no GitHub para apoiar *code review* de cenários de teste de API, quando necessário.

---

## 📌 Próximos passos (opcional)

- Adicionar novas collections oficiais de outras APIs nesta mesma integração, cada uma com seu próprio arquivo `.postman_collection.json`.
- Padronizar a estrutura de pastas para algo como:

```text
Postman Collections/
├── core-api.postman_collection.json
├── auth-api.postman_collection.json
└── payments-api.postman_collection.json
```

- Evoluir o fluxo para uso de branches e Pull Requests para mudanças maiores nas collections, se o time desejar um nível extra de governança.

---
