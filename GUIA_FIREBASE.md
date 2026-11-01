# Guia: pôr o Macaquinho Brincalhão online (grátis)

Este guia é para quem nunca fez isto. Demora cerca de 30 minutos.
Tudo usa o **plano gratuito Spark** do Firebase, que não pede cartão de crédito.

> A consola do Firebase pode aparecer em português ou em inglês.
> Ponho os dois nomes quando são diferentes, por exemplo: **Criar projeto** *(Create a project)*.

---

## (a) Criar o projeto Firebase

1. Abra <https://console.firebase.google.com> e entre com a sua conta Google.
2. Carregue em **Criar projeto** *(Create a project)*.
3. Dê um nome, por exemplo `macaquinho-terapia`, e carregue em **Continuar**.
4. Quando perguntar pelo **Google Analytics**, **desligue-o** (não é preciso) e carregue em **Criar projeto**.
5. Espere um pouco e carregue em **Continuar**. Já está no seu projeto.

O plano é o **Spark (gratuito)** por defeito. Não mude.

---

## (b) Ativar o Firestore e o Authentication

### Firestore (a base de dados)

1. No menu da esquerda: **Criação** *(Build)* → **Firestore Database**.
2. Carregue em **Criar base de dados** *(Create database)*.
3. **Localização:** escolha uma na Europa, por exemplo `eur3 (europe)` ou `europe-west1`.
   ⚠️ Esta escolha não se pode mudar depois.
4. Escolha **Iniciar no modo de produção** *(Start in production mode)* e carregue em **Criar**.
5. As regras de segurança vão ser coladas no passo (c), depois de criar a sua conta.

### Authentication (o login do terapeuta)

1. No menu da esquerda, em **Categorias dos produtos**: **Segurança** → **Authentication** → **Vamos começar** *(Get started)*.
   (Em consolas mais antigas está em **Criação** *(Build)* → **Authentication**.)
2. No separador **Método de login** *(Sign-in method)*, escolha **E-mail/senha** *(Email/Password)*.
3. Ligue **só o primeiro interruptor** (E-mail/senha) e carregue em **Salvar**.
4. **Importante para a segurança:** vá ao separador **Configurações** *(Settings)* → **Ações do usuário** *(User actions)*
   e **desmarque** "Ativar criação (inscrição)" *(Enable create (sign-up))*. Carregue em **Salvar**.
   Assim, ninguém consegue criar contas sozinho. Só existe a sua.

---

## (c) Criar a sua conta de terapeuta (e colar as regras)

1. Em **Authentication** → separador **Utilizadores** *(Users)* → **Adicionar utilizador** *(Add user)*.
2. Escreva o seu email e uma palavra-passe forte, e carregue em **Adicionar utilizador**.
3. Na lista aparece a sua conta. **Copie o "UID do utilizador"** *(User UID)*, que é uma sequência longa de letras e números.
4. Abra o ficheiro **`firestore.rules`** (está ao lado do `index.html`) e troque
   `COLE_AQUI_O_SEU_UID` pelo UID que copiou. Mantenha as aspas.
5. Na consola: **Firestore Database** → separador **Regras** *(Rules)*.
   Apague tudo o que lá está, cole **todo** o conteúdo do `firestore.rules` e carregue em **Publicar** *(Publish)*.

---

## (d) Colar a configuração no HTML

1. Na consola, carregue na **roda dentada ⚙️** (ao lado de "Visão geral do projeto") → **Definições do projeto** *(Project settings)*.
2. Desça até **As suas apps** *(Your apps)* e carregue no ícone **`</>`** (Web).
3. Dê um nome à app, por exemplo `macaquinho-web`. **Não** marque o Firebase Hosting. Carregue em **Registar app**.
4. Aparece um bloco de código com `const firebaseConfig = { apiKey: "...", ... }`.
5. Abra o `index.html` no editor. Logo no início está o bloco `window.FIREBASE_CONFIG`.
   Troque cada `COLE_AQUI` pelo valor correspondente: `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId` e `appId`.
6. Guarde o ficheiro.

> **É normal** a `apiKey` ficar visível no HTML. No Firebase ela não é secreta.
> O que protege os dados são as **regras** do passo (c).

**Testar no computador:** abra o `index.html`, entre na **Área do Terapeuta** com o email e a palavra-passe do passo (c).
Debaixo do título deve aparecer "☁️ Dados online (Firebase)".

---

## (e) Publicar de graça e obter o link

O seu projeto já está no GitHub (`luanaalmeida13/macaquinho-ginastica`), por isso o mais simples é o **GitHub Pages**.

### 1. Enviar os ficheiros para o GitHub

**Opção fácil (no site):**

1. Abra <https://github.com/luanaalmeida13/macaquinho-ginastica>.
2. Carregue em **Add file** → **Upload files**.
3. Arraste o `index.html` (e, se quiser, o `firestore.rules` e este guia).
4. Carregue em **Commit changes**.

**Opção pelo terminal:** abra o terminal dentro da pasta `macaquinho-ginastica` e escreva:

```bash
git add index.html firestore.rules GUIA_FIREBASE.md
```

```bash
git commit -m "Macaquinho com Firebase, pacientes e atribuição"
```

```bash
git push
```

### 2. Ligar o GitHub Pages

1. No repositório, carregue em **Settings** → **Pages** (menu da esquerda).
2. Em **Source**, escolha **Deploy from a branch**.
3. Em **Branch**, escolha **main** e a pasta **/ (root)**, e carregue em **Save**.
4. Espere 1 a 2 minutos e atualize a página. Aparece o link:

   **<https://luanaalmeida13.github.io/macaquinho-ginastica/>**

### 3. Autorizar esse endereço no Firebase

Na consola: **Authentication** → **Definições** *(Settings)* → **Domínios autorizados** *(Authorized domains)*
→ **Adicionar domínio** → `luanaalmeida13.github.io`.

### 4. Dar o link aos pacientes

- Envie aos pais **o link** e **o código** da criança (ex.: `JOAO-4821`).
- No telemóvel ou tablet, abram o link e carreguem em **🔑 Tenho um código**.
- Dica: no menu do navegador, **"Adicionar ao ecrã principal"** cria um ícone como se fosse uma app.
- O aparelho lembra-se do código. Da próxima vez, a criança vai direta aos seus exercícios.

> **Alternativa: Firebase Hosting.** Também é gratuito, mas precisa de instalar o Node.js e usar o terminal
> (`npm install -g firebase-tools`, `firebase login`, `firebase init hosting`, `firebase deploy`).
> Como já tem o GitHub, o GitHub Pages é mais simples.

---

## Como funciona sem internet

- Quando a criança entra com o código, a lista de exercícios fica guardada no aparelho.
- Se a internet falhar, a criança continua a jogar. Cada exercício concluído fica numa fila e é enviado
  sozinho quando a ligação voltar (aparece "⏳ … à espera de internet").
- Para o jogo **abrir** sem internet, a página tem de ter sido aberta com internet pelo menos uma vez nesse aparelho
  (e o navegador tem de a ter em cache).

## Privacidade

- Guarde apenas o **primeiro nome** e o **código**. Não guarde apelido, data de nascimento nem diagnóstico.
- Quem souber um código consegue ver o primeiro nome e a lista de exercícios desse paciente, e nada mais.
  Não partilhe os códigos publicamente.
- Ao apagar um paciente, apagam-se também o código e todo o progresso dele.
