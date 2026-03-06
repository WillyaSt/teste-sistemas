# Plano de Teste – Sistema SRL

## 1. Escopo

Este plano de teste cobre os seguintes módulos do Sistema de Reservas de Laboratório (SRL):

- **Módulo de Autenticação**: Registro e login de usuários (ADMIN e USER)
- **Módulo de Salas**: Cadastro e listagem de salas de laboratório
- **Módulo de Reservas**: Criação e listagem de reservas de salas
- **Módulo de Incidentes**: Abertura e fechamento de incidentes técnicos

O teste abrangerá:
- Validação de funcionalidades (12 Requisitos Funcionais)
- Validação de regras de negócio (12 Regras de Negócio)
- Controle de acesso e permissões (perfis ADMIN e USER)
- Validação de respostas HTTP e tratamento de erros

**Fora do escopo**: Interface gráfica (o sistema é apenas API REST)

---

## 2. Objetivo

Garantir que o Sistema de Reservas de Laboratório atenda todos os requisitos funcionais e regras de negócio especificados, validando:

- Correto funcionamento de todos os endpoints da API
- Aplicação adequada de permissões por perfil de usuário
- Validação de dados de entrada conforme especificado
- Tratamento apropriado de erros e exceções
- Segurança através de autenticação por token JWT
- Integridade dos dados e regras de negócio (unicidade, conflitos de horário, validações)

---

## 3. Estratégia de Teste

### 3.1 Tipos de Teste

**Testes Funcionais**
- Validação de cada requisito funcional (RF01 a RF12)
- Testes de fluxo completo (registro → login → operações)

**Testes de Regras de Negócio**
- Validação de todas as regras (RN01 a RN12)
- Testes de validação de dados (email único, senha forte, horários válidos)
- Testes de conflito de reservas

**Testes de Segurança**
- Autenticação e autorização
- Controle de acesso por perfil (ADMIN vs USER)
- Proteção de endpoints com token JWT

**Testes Negativos**
- Tentativas de acesso sem autenticação
- Tentativas de operações sem permissão
- Dados inválidos ou incompletos

### 3.2 Abordagem

- **Testes manuais** via ferramentas como Postman ou Insomnia
- **Testes automatizados** utilizando framework pytest
- Testes serão executados em ordem de dependência (autenticação → demais módulos)

---

## 4. Ambiente

### 4.1 Ambiente de Teste

- **Sistema Operacional**: Windows
- **Python**: Versão 3.8 ou superior
- **Framework**: FastAPI
- **Banco de Dados**: SQLite (ambiente de teste)
- **Servidor**: Uvicorn (servidor ASGI)

### 4.2 Ferramentas

- **Cliente HTTP**: Postman, Insomnia ou curl
- **Framework de Testes**: pytest
- **Documentação Automática**: Swagger UI (FastAPI)
- **Controle de Versão**: Git

### 4.3 Configuração

- API rodando em `http://localhost:8000`
- Banco de dados isolado para testes


## 5. Critérios de Entrada

Para iniciar a execução dos testes, os seguintes critérios devem ser atendidos:

- ✅ Código-fonte completo e disponível
- ✅ Ambiente de desenvolvimento configurado (Python + dependências)
- ✅ Banco de dados criado e acessível
- ✅ API inicializável sem erros
- ✅ Documento de requisitos aprovado e disponível
- ✅ Casos de teste documentados
- ✅ Ferramentas de teste instaladas e configuradas

---

## 6. Critérios de Saída

Os testes serão considerados concluídos quando:

- ✅ Todos os casos de teste planejados foram executados
- ✅ Todos os requisitos funcionais (RF01-RF12) foram validados
- ✅ Todas as regras de negócio (RN01-RN12) foram testadas
- ✅ Taxa de sucesso mínima de 95% nos testes funcionais
- ✅ Todos os bugs críticos e de alta prioridade foram corrigidos
- ✅ Documentação de bugs e falhas gerada
- ✅ Relatório final de testes elaborado
- ✅ Aprovação do responsável técnico

---

## 7. Responsáveis

| Papel | Responsabilidade | Nome/Equipe |
|-------|------------------|-------------|
| **Analista de Testes** | Planejamento e documentação dos testes | Equipe de QA |
| **Testador** | Execução dos casos de teste | Equipe de QA |
| **Desenvolvedor** | Correção de bugs identificados | Equipe de Desenvolvimento |
| **Tech Lead** | Revisão e aprovação dos resultados | Líder Técnico |
| **Product Owner** | Validação de requisitos e aceite final | Gerente de Produto |

---

**Data de Criação**: 06/03/2026  
**Versão**: 1.0