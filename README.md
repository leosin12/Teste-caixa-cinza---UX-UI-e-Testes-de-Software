# ATIVIDADE INDIVÍDUAL — TESTE CAIXA CINZA COM SUPABASE E POSTMAN

## Introdução
Este repositório documenta a atividade prática de testes funcionais de caixa cinza em APIs de autenticação. O projeto integra o ecossistema de backend em nuvem do **Supabase** para gerenciar o banco de dados e usuários, e a ferramenta **Postman** para a validação e execução de requisições HTTP e cenários de teste.

## Objetivo da Atividade
Compreender e aplicar testes de caixa cinza em APIs de autenticação, configurando um ambiente em nuvem no Supabase, estruturando variáveis e requisições no Postman, e validando tanto o comportamento de sucesso (login válido) quanto as respostas de erro diante de entradas inválidas.

# Configuração do Supabase
* **Criação do Projeto:** Foi criado um projeto na plataforma Supabase na região de São Paulo (`sa-east-1`), nomeado como "Teste Caixa Cinza".
* **Autenticação:** O provedor de E-mail/Senha foi habilitado no módulo de autenticação (`Authentication > Sign In / Providers`).
* **Usuário de Teste:** Foi cadastrado manualmente um usuário válido (`teste.user@email.com`) para servir de base nas validações de acesso.
* **Credenciais:** Foram obtidas a URL da API (`base_url`) e a chave pública de acesso (`api_key`).

## Configuração do Postman
* **Workspace:** Foi criado um Workspace dedicado no Postman para organizar os testes da API.
* **Environment:** Foi configurado um ambiente de variáveis (`Supabase testes`) contendo:
  * `base_url`: URL do projeto no Supabase.
  * `api_key`: Chave pública da API.
  * `email`: E-mail do usuário de teste.
  * `password`: Senha cadastrada.
* **Finalidade:** Permitir a reutilização dinâmica de dados sensíveis e parâmetros de conexão nas requisições.

## Configuração das Requisições
* **Endpoint:** `POST {{base_url}}/auth/v1/token?grant_type=password`
* **Headers:** 
  * `apikey`: `{{api_key}}`
  * `Content-Type`: `application/json`
* **Body JSON:** 
  ```json
  {
    "email": "{{email}}",
    "password": "{{password}}"
  }

## Execução dos Testes
Foram executados cenários cobrindo fluxos positivos e negativos:
Login Válido: Envio de e-mail e senha corretos, obtendo status HTTP 200 e o retorno do access_token.
Login Inválido: Envio de credenciais incorretas, obtendo status HTTP 400 e a mensagem de erro de autenticação.

## Registro dos Testes
Os testes foram estruturados e mapeados para garantir a rastreabilidade:
ID do Teste / Cenário: Validados individualmente na collection do Postman (Request 01 e Request 02).
Entradas vs. Saídas: Comparação rigorosa entre os dados enviados e os códigos de status retornados (200 OK para sucesso e 400 Bad Request para falhas de credenciais).
Importância: A documentação dos registros assegura a validação da segurança e o correto tratamento de exceções pela API.

## Resultados Obtidos
A API respondeu corretamente aos estímulos planejados.
O cenário com credenciais válidas emitiu com sucesso o token de acesso e os dados do usuário.
O cenário com credenciais incorretas bloqueou o acesso adequadamente, retornando o código 400 com a mensagem descritiva de falha de credenciais.
