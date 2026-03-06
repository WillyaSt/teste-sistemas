# Sistema de Reservas de Laboratório (SRL)

## 📖 Descrição

Sistema de gerenciamento de reservas de laboratórios para instituições de ensino. Desenvolvido como projeto educacional para ensino de **metodologias de teste de software**.

## 🎯 Objetivo Educacional

Este projeto é um **laboratório prático** para ensinar:
- Documentação de requisitos
- Planejamento de testes
- Criação de casos de teste
- Testes manuais com Postman
- Rastreabilidade de requisitos
- Registro e gestão de bugs

---

## 🚀 Tecnologias

- **Python 3.8+**
- **FastAPI** - Framework web
- **SQLAlchemy** - ORM
- **SQLite** - Banco de dados
- **Pydantic** - Validação de dados
- **Uvicorn** - Servidor ASGI

---

## 📁 Estrutura do Projeto

```
teste-sistemas/
│
├── routers/              # Rotas da API (auth, rooms, bookings, incidents)
├── docs/                 # Documentação
│   ├── 01_requisitos/    # Especificação de requisitos
│   ├── 02_api/           # Plano de teste
│   ├── 03_casos_de_teste/# Casos de teste detalhados
│   ├── 04_matriz_rastreabilidade/
│   ├── 05_registro_de_falhas/
│   ├── GUIA_TESTES_POSTMAN.md       # 📖 Tutorial completo
│   ├── QUICK_START_POSTMAN.md       # ⚡ Início rápido
│   ├── SRL_Postman_Collection.json  # 📦 Collection importável
│   └── SRL_Postman_Environment.json # ⚙️ Variáveis de ambiente
│
├── main.py              # Aplicação principal
├── models.py            # Modelos do banco de dados
├── schemas.py           # Schemas de validação
├── database.py          # Configuração do banco
├── auth.py              # Autenticação e autorização
└── requirements.txt     # Dependências
```

---

## ⚙️ Instalação

### 1. Clonar o Repositório
```powershell
cd "C:\Users\israe\OneDrive\Área de Trabalho"
git clone <url-do-repo>
cd teste-sistemas
```

### 2. Criar Ambiente Virtual
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

### 3. Instalar Dependências
```powershell
pip install -r requirements.txt
```

### 4. Iniciar a API
```powershell
python -m uvicorn main:app --reload
```

✅ API disponível em: **http://localhost:8000**

---

## 🧪 Testes com Postman

### 🎓 Para Alunos

#### ⚡ Início Rápido (5 minutos)
1. Siga o guia: **[docs/QUICK_START_POSTMAN.md](docs/QUICK_START_POSTMAN.md)**
2. Importe os arquivos:
   - `docs/SRL_Postman_Collection.json` (30 casos de teste prontos)
   - `docs/SRL_Postman_Environment.json` (variáveis configuradas)
3. Execute os testes!

#### 📖 Tutorial Completo
Para entender cada teste em detalhes: **[docs/GUIA_TESTES_POSTMAN.md](docs/GUIA_TESTES_POSTMAN.md)**

Inclui:
- ✅ 27 cenários de teste passo a passo
- ✅ Scripts de automação
- ✅ Testes positivos e negativos
- ✅ Atividades práticas
- ✅ Troubleshooting

---

## 📚 Documentação de Teste

| Documento | Descrição |
|-----------|-----------|
| [requisitos.md](docs/01_requisitos/requisitos.md) | Especificação completa de requisitos (RF e RN) |
| [plano_de_teste.md](docs/02_api/plano_de_teste.md) | Plano de teste (escopo, estratégia, critérios) |
| [casos_de_teste.md](docs/03_casos_de_teste/casos_de_teste.md) | 34 casos de teste detalhados |
| [GUIA_TESTES_POSTMAN.md](docs/GUIA_TESTES_POSTMAN.md) | Tutorial completo de testes manuais |
| [QUICK_START_POSTMAN.md](docs/QUICK_START_POSTMAN.md) | Guia rápido de início |

---

## 🔑 Funcionalidades

### Módulos
1. **Autenticação** - Registro e login de usuários (ADMIN/USER)
2. **Salas** - Cadastro e listagem de laboratórios
3. **Reservas** - Agendamento com validação de conflitos
4. **Incidentes** - Abertura e fechamento de problemas técnicos

### Perfis de Usuário
| Operação | ADMIN | USER |
|----------|-------|------|
| Registrar usuário | ✔ | ✔ |
| Criar sala | ✔ | ✖ |
| Listar salas | ✔ | ✔ |
| Criar reserva | ✔ | ✔ |
| Listar próprias reservas | ✔ | ✔ |
| Abrir incidente | ✔ | ✔ |
| Fechar incidente | ✔ | ✖ |

---

## 🌐 Endpoints da API

### Autenticação
- `POST /auth/register` - Registrar usuário
- `POST /auth/login` - Login e obtenção de token

### Salas
- `POST /rooms` - Criar sala (ADMIN)
- `GET /rooms` - Listar salas

### Reservas
- `POST /bookings` - Criar reserva
- `GET /bookings/my` - Listar minhas reservas

### Incidentes
- `POST /incidents` - Abrir incidente
- `PATCH /incidents/{id}/close` - Fechar incidente (ADMIN)

### Documentação Interativa
- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

---

## 👨‍🏫 Para Professores

### Plano de Aula Sugerido

#### Aula 1: Requisitos e Planejamento (2h)
- Apresentar requisitos funcionais e regras de negócio
- Discutir plano de teste
- Exercício: identificar cenários de teste adicionais

#### Aula 2: Casos de Teste (2h)
- Revisar casos de teste documentados
- Praticar escrita de novos casos
- Exercício: criar casos de teste para novos requisitos

#### Aula 3: Testes Manuais com Postman (3h)
- Configurar Postman e importar collection
- Executar testes funcionais
- Documentar resultados
- Exercício: executar todos os 30 casos de teste

#### Aula 4: Análise de Resultados (2h)
- Discutir bugs encontrados
- Preencher matriz de rastreabilidade
- Relatório final de testes

### Atividades Avaliativas
1. **Execução de Testes** (30%) - Executar todos os casos de teste e documentar
2. **Criação de Casos** (25%) - Criar 5 novos casos de teste
3. **Encontrar Bugs** (20%) - Identificar e documentar bugs
4. **Relatório Final** (25%) - Análise de cobertura e recomendações

---

## 🎓 Exercícios para Alunos

### Nível Básico
- [ ] Executar todos os casos de teste da collection
- [ ] Documentar resultados em planilha
- [ ] Identificar diferenças entre testes positivos e negativos

### Nível Intermediário
- [ ] Criar 5 novos casos de teste não documentados
- [ ] Testar cenários de borda (edge cases)
- [ ] Validar todas as mensagens de erro

### Nível Avançado
- [ ] Criar scripts de automação no Postman
- [ ] Executar teste de carga (múltiplas reservas simultâneas)
- [ ] Propor melhorias na API

---

## 🐛 Troubleshooting

### API não inicia
```powershell
# Verificar Python instalado
python --version

# Reinstalar dependências
pip install -r requirements.txt --force-reinstall
```

### Banco de dados corrompido
```powershell
# Deletar e reiniciar
Remove-Item lab_system.db
python -m uvicorn main:app --reload
```

### Porta 8000 em uso
```powershell
# Usar porta diferente
python -m uvicorn main:app --reload --port 8001
```
Lembrar de atualizar `base_url` no Postman!

---

## 📈 Cobertura de Testes

- ✅ **12 Requisitos Funcionais** - 100% cobertos
- ✅ **12 Regras de Negócio** - 100% cobertas
- ✅ **8 Endpoints** - 100% testados
- ✅ **34 Casos de Teste** - Positivos e negativos
- ✅ **Autenticação e Autorização** - Totalmente validados

---

## 🤝 Contribuindo

Este é um projeto educacional. Sugestões de melhorias são bem-vindas!

1. Fork o projeto
2. Crie uma branch para sua feature
3. Commit suas mudanças
4. Push para a branch
5. Abra um Pull Request

---

## 📄 Licença

Este projeto é desenvolvido para fins educacionais.

---

## 📧 Contato

Para dúvidas sobre o projeto ou metodologia de ensino, entre em contato.

---

**Desenvolvido com 💙 para ensino de Teste de Sistemas**