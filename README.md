# DePhs-social_network

Uma plataforma social pessoal na nuvem. Criada como projeto de portfólio para mostrar habilidades **full-stack, cloud e planejamento de projetos**.

Usuários podem **registrar-se, fazer login, criar posts** na primeira versão. O projeto utiliza **Neo4j**, **NodeJS serverless (Vercel Functions)** e **React + TailwindCSS**.

---

## Índice

- [Tecnologias](#tecnologias)  
- [Arquitetura](#arquitetura)  
- [Funcionalidades](#funcionalidades)  
- [Esquema do Grafo](#esquema-do-grafo)  
- [Como Rodar](#como-rodar)  
- [CI/CD](#cicd)  
- [Melhorias Futuras](#melhorias-futuras)

---

## Tecnologias

**Frontend:**  
- React (SPA)  
- TailwindCSS  
- Hospedagem: **Vercel (static site + serverless functions)**  

**Backend:**  
- NodeJS  
- **Serverless Functions (Vercel)**  
- API via HTTP endpoints  

**Banco de Dados:**  
- Neo4j AuraDB Free (Banco de Grafos)  

**CI/CD:**  
- GitHub Actions (build e deploy automáticos)  

---

## Arquitetura


[React SPA - Vercel]
|
v
[Serverless Functions - Vercel]
|
v
[Neo4j AuraDB Free]


**Fluxo:**  

1. Usuário interage com a SPA React  
2. Frontend chama as serverless functions  
3. NodeJS executa a lógica de negócio  
4. Neo4j armazena e recupera dados de usuários, posts e relações  
5. API retorna JSON  
6. React renderiza os resultados dinamicamente  

> O hosting estático (Vercel) serve apenas os arquivos do frontend; toda lógica dinâmica fica nas serverless functions.

---

## Funcionalidades

### Autenticação
- Registro de usuário (email, nome e senha)  
- Senha criptografada (bcrypt)  
- Login com JWT  
- Middleware para rotas protegidas  

### Posts
- Criar posts com título, conteúdo e tags  
- Posts ligados aos usuários no grafo Neo4j  

### Funcionalidades Extras
- SPA com React + TailwindCSS  
- Backend serverless NodeJS via Vercel Functions  
- Modelagem de grafos com Neo4j  
- CI/CD automático via GitHub Actions  

---

## Esquema do Grafo

```cypher
(:User {id, name, email, passwordHash, createdAt})
(:Post {id, title, content, createdAt})
(:Tag {name})

(:User)-[:POSTED]->(:Post)
(:Post)-[:HAS_TAG]->(:Tag)
(:User)-[:LIKED]->(:Post)
