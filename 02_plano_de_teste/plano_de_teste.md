# Plano de Teste – Sistema SRL

## 1. Escopo

## O presente plano de teste abrange todas as funcionalidades descritas no Documento de Requisitos versão 1.0 do Sistema de Reservas de Laboratório (SRL), incluindo:

* **Módulo de Autenticação (Registro e Login);**

* **Módulo de Salas;**

* **Módulo de Reservas;**

* **Módulo de Incidentes;**

* **Validação das Regras de Negócio (RN01 a RN12);**

* **Verificação de segurança e controle de acesso baseado em perfis (ADMIN e USER).**

* **Este plano contempla testes funcionais, validações de regras de negócio e testes de autorização da API REST.**

## 2. Objetivo

## Garantir que a API REST do Sistema SRL:

* **Processe corretamente todas as requisições;**

* **Respeite as regras de negócio definidas;**

* **Valide corretamente restrições de horário e conflitos de reserva;**

* **Aplique corretamente as permissões por perfil (ADMIN e USER);**

## Retorne os códigos de status HTTP apropriados, tais como:

* **201 Created**

* **200 OK**

* **400 Bad Request**

* **401 Unauthorized**

* **403 Forbidden**

* **404 Not Found**

* **409 Conflict**

* **O objetivo é assegurar a conformidade do sistema com o documento de requisitos e garantir sua confiabilidade e segurança.**

## 3. Estratégia de Teste

* **A estratégia de teste adotada consiste na execução manual dos endpoints da API por meio da ferramenta Swagger, enviando requisições e validando as respostas retornadas pelo sistema.**

## Serão aplicados dois tipos principais de teste:

* **Testes de Sucesso**

* **Envio de dados válidos e completos para verificar se o sistema processa corretamente a operação e retorna o status esperado.**

* **Testes de Erro**

## Envio de dados inválidos ou que violem regras de negócio (exemplo: senha fora do padrão, horário inválido, tentativa de ação sem permissão), com o objetivo de verificar se o sistema:

* **Bloqueia a operação;**

* **Retorna mensagem descritiva;**

* **Responde com o código HTTP adequado.**

## 4. Ambiente

## Ferramentas utilizadas:

* **Swagger (para execução das requisições)**

* **Banco de dados de teste**

## Configuração:

* **API executando em ambiente local**

* **Autenticação via token JWT**

## Padrão de dados:

* **Datas no formato ISO (YYYY-MM-DD)**

* **Horários no formato HH:MM (24h)**

## 5. Critérios de Entrada

## Os testes serão iniciados quando:

* **O Documento de Requisitos versão 1.0 estiver definido;**

* **O código do sistema estiver implementado e compilando sem erros;**

* **A API estiver em execução no ambiente local;**

* **O banco de dados de teste estiver configurado.**

## 6. Critérios de Saída

## Os testes serão considerados concluídos quando:

* **100% dos casos de teste planejados forem executados;**

* **Não houver erros críticos relacionados à segurança ou regras de negócio;**

* **Todas as validações de permissão e autenticação estiverem funcionando corretamente;**

* **Os códigos de status HTTP estiverem sendo retornados conforme esperado.**

* **Caso sejam identificados defeitos críticos, os testes deverão ser reexecutados após correção.**

## 7. Responsáveis

## Desenvolvedor / Executor dos Testes:
* **Willyam Douglas Gomes Soares**

## Revisor:
* **Israel de Marcos Ferreira da Silva**
