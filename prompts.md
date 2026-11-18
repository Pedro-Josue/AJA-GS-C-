# Registro de prompts de inteligência artificial

Este arquivo reúne os prompts consolidados usados com inteligência artificial como copiloto para aprender, estruturar e revisar o projeto AJA. A equipe analisou as sugestões antes de aplicá-las e permaneceu responsável pelas decisões, pelo código e pelos testes. Os textos foram organizados para facilitar a explicação durante a avaliação e não contêm dados pessoais reais, senhas privadas, tokens ou chaves de produção.

## 1. Delimitação da CitizenTech

**Prompt**

> Atue como orientador de produto e ajude a delimitar uma CitizenTech acadêmica chamada AJA - Acessibilidade, Justiça e Ação. A solução deve apoiar cidadãos no registro e acompanhamento de barreiras de acessibilidade urbana em São Paulo, usando apenas dados simulados. Proponha um problema em uma frase, público beneficiado, jornada principal, indicadores de impacto e relação com os ODS 10 e 11. Mantenha o escopo simples o suficiente para ser implementado como uma Web API.

**Finalidade e aplicação no projeto:** o prompt ajudou a transformar a ideia geral em uma jornada objetiva: criar conta, registrar demanda, apoiar, comentar e acompanhar a atualização administrativa. A equipe revisou o resultado e adotou indicadores relacionados a demandas, participações e mudanças de situação.

## 2. Modelagem orientada a objetos

**Prompt**

> Considere uma aplicação C#/.NET para demandas de acessibilidade com as entidades Demanda, Apoio, Comentario e HistoricoSituacao. Sugira uma modelagem orientada a objetos que proteja o estado das entidades e concentre as regras de negócio em métodos, evitando classes que sejam apenas recipientes de propriedades. Inclua regras para edição, remoção lógica, apoio idempotente, moderação de comentário e mudança de situação com justificativa. Explique quais invariantes devem ser testadas.

**Finalidade e aplicação no projeto:** a resposta foi usada como referência para manter propriedades com alteração controlada e criar comportamentos como editar, remover, registrar apoio e atualizar a situação. As invariantes sugeridas foram conferidas nos testes unitários.

## 3. Interfaces e injeção de dependência

**Prompt**

> Revise a arquitetura de uma ASP.NET Core Web API dividida nos módulos Auth, Demandas e Participacoes. Proponha interfaces para os casos de uso e mostre como controllers podem depender de abstrações por injeção de dependência, sem acessar diretamente o Entity Framework Core. Explique a responsabilidade de API, Application, Domain e Infrastructure e aponte sinais de acoplamento indevido.

**Finalidade e aplicação no projeto:** o prompt orientou a separação entre controllers, contratos de aplicação, entidades e implementações técnicas. A equipe aplicou `IAuthService`, `IDemandaService` e `IParticipacaoService` e registrou as implementações no contêiner do ASP.NET Core.

## 4. Entity Framework Core e LINQ

**Prompt**

> Para uma API C# com Entity Framework Core e SQLite, proponha o mapeamento das entidades Demanda, Apoio, Comentario e HistoricoSituacao. Considere chaves estrangeiras, índices, unicidade de apoio por usuário e demanda, remoção lógica e migrações. Depois, sugira consultas LINQ assíncronas para filtrar demandas por situação, categoria, bairro e autoria, com ordenação e paginação. Não use avaliação em memória quando a consulta puder ser executada no banco.

**Finalidade e aplicação no projeto:** as sugestões apoiaram a configuração relacional, os índices, a restrição de apoio único, as migrações e as consultas combináveis. A equipe confirmou o comportamento com testes de integração executados sobre SQLite.

## 5. API REST e programação assíncrona

**Prompt**

> Analise o contrato de uma Web API versionada em `/api/v1` para autenticação, demandas, apoios e comentários. Sugira métodos HTTP, rotas, códigos de resposta e formato de erro Problem Details. Verifique também se controllers e serviços usam `async/await`, propagam `CancellationToken` e evitam `.Result` e `.Wait()`. Preserve regras de autoria e operações exclusivas de Admin.

**Finalidade e aplicação no projeto:** o resultado serviu para revisar rotas e respostas como `201`, `200`, `204`, `400`, `401`, `403`, `404` e `409`. A equipe também verificou a propagação assíncrona até as operações do EF Core e do ASP.NET Core Identity.

## 6. Estratégia de testes

**Prompt**

> Crie uma estratégia de testes para esta aplicação C# sem substituir a análise da equipe. Liste casos unitários para as regras das entidades e casos de integração para cadastro, login JWT, autorização por role e autoria, persistência SQLite, filtros LINQ, paginação e migrações. Para cada caso, indique cenário, ação e resultado esperado, incluindo fluxos de sucesso e falha.

**Finalidade e aplicação no projeto:** o prompt foi convertido em testes xUnit. Foram cobertas regras de domínio e fluxos HTTP reais, incluindo tokens inválidos, respostas `401` e `403`, persistência, índices e geração do documento OpenAPI.

## 7. Revisão de qualidade, segurança e documentação

**Prompt**

> Atue como revisor final de um repositório acadêmico C#/.NET. Verifique clareza de nomes, responsabilidades pequenas, ausência de duplicação relevante, tratamento seguro de erros, proteção de segredos, configuração JWT, conta de demonstração restrita ao ambiente Development, Swagger e instruções reproduzíveis no README. Aponte somente problemas verificáveis e proponha correções objetivas. Considere também a necessidade de evidências visuais da aplicação em execução.

**Finalidade e aplicação no projeto:** a revisão apoiou ajustes na segurança, no `.gitignore`, na documentação da conta de demonstração e nas instruções de execução. Também orientou a inclusão das evidências do Swagger, do health check e de uma consulta autenticada, todas registradas sem exibir o token JWT.
