# Casos de Teste – Sistema SRL

---

## Módulo 1: Autenticação

### CT01 – Registrar usuário com sucesso
**Requisito:** RF01, RN01, RN02  
**Descrição:** Validar registro de novo usuário com dados válidos  
**Pré-condição:** Nenhuma  
**Entrada:**
```json
{
  "name": "João Silva",
  "email": "joao@teste.com",
  "password": "senha123",
  "role": "USER"
}
```
**Resultado Esperado:** Status 201, usuário criado com sucesso

---

### CT02 – Registrar usuário com email duplicado
**Requisito:** RN01  
**Descrição:** Validar rejeição de email já cadastrado  
**Pré-condição:** Email "joao@teste.com" já cadastrado  
**Entrada:**
```json
{
  "name": "Maria Santos",
  "email": "joao@teste.com",
  "password": "senha456",
  "role": "USER"
}
```
**Resultado Esperado:** Status 400, mensagem "Email já cadastrado."

---

### CT03 – Registrar usuário com senha fraca
**Requisito:** RN02  
**Descrição:** Validar rejeição de senha sem número  
**Pré-condição:** Nenhuma  
**Entrada:**
```json
{
  "name": "Pedro Costa",
  "email": "pedro@teste.com",
  "password": "senhafraca",
  "role": "USER"
}
```
**Resultado Esperado:** Status 422, mensagem "Senha deve conter pelo menos 1 número."

---

### CT04 – Registrar usuário com senha curta
**Requisito:** RN02  
**Descrição:** Validar rejeição de senha com menos de 8 caracteres  
**Pré-condição:** Nenhuma  
**Entrada:**
```json
{
  "name": "Ana Lima",
  "email": "ana@teste.com",
  "password": "abc123",
  "role": "ADMIN"
}
```
**Resultado Esperado:** Status 422, mensagem "Senha deve ter no mínimo 8 caracteres."

---

### CT05 – Login com credenciais válidas
**Requisito:** RF02, RF03  
**Descrição:** Validar login bem-sucedido e retorno de token  
**Pré-condição:** Usuário "joao@teste.com" cadastrado  
**Entrada:**
```json
{
  "email": "joao@teste.com",
  "password": "senha123"
}
```
**Resultado Esperado:** Status 200, retorno de token JWT válido

---

### CT06 – Login com senha incorreta
**Requisito:** RF02  
**Descrição:** Validar rejeição de credenciais inválidas  
**Pré-condição:** Usuário "joao@teste.com" cadastrado  
**Entrada:**
```json
{
  "email": "joao@teste.com",
  "password": "senhaerrada"
}
```
**Resultado Esperado:** Status 401, mensagem "Email ou senha inválidos."

---

### CT07 – Login com email não cadastrado
**Requisito:** RF02  
**Descrição:** Validar rejeição de email inexistente  
**Pré-condição:** Nenhuma  
**Entrada:**
```json
{
  "email": "inexistente@teste.com",
  "password": "senha123"
}
```
**Resultado Esperado:** Status 401, mensagem "Email ou senha inválidos."

---

## Módulo 2: Salas

### CT08 – Criar sala como ADMIN
**Requisito:** RF04, RN04, RN05  
**Descrição:** Validar criação de sala por usuário ADMIN  
**Pré-condição:** Usuário ADMIN autenticado  
**Entrada:**
```json
{
  "name": "Lab 101",
  "capacity": 30,
  "resources": ["projetor", "ar-condicionado", "computadores"]
}
```
**Resultado Esperado:** Status 201, sala criada com sucesso

---

### CT09 – Criar sala como USER
**Requisito:** RN03, Permissões  
**Descrição:** Validar bloqueio de criação de sala por USER  
**Pré-condição:** Usuário USER autenticado  
**Entrada:**
```json
{
  "name": "Lab 102",
  "capacity": 25,
  "resources": ["projetor"]
}
```
**Resultado Esperado:** Status 403, mensagem "Acesso restrito a administradores."

---

### CT10 – Criar sala sem autenticação
**Requisito:** RN03  
**Descrição:** Validar bloqueio de acesso sem token  
**Pré-condição:** Nenhuma  
**Entrada:**
```json
{
  "name": "Lab 103",
  "capacity": 20,
  "resources": []
}
```
**Resultado Esperado:** Status 401, mensagem "Token inválido ou ausente."

---

### CT11 – Criar sala com nome duplicado
**Requisito:** RN04  
**Descrição:** Validar rejeição de nome já existente  
**Pré-condição:** ADMIN autenticado, sala "Lab 101" já existe  
**Entrada:**
```json
{
  "name": "Lab 101",
  "capacity": 15,
  "resources": ["quadro"]
}
```
**Resultado Esperado:** Status 400, mensagem "Nome da sala já existe."

---

### CT12 – Criar sala com capacidade zero
**Requisito:** RN05  
**Descrição:** Validar rejeição de capacidade inválida  
**Pré-condição:** ADMIN autenticado  
**Entrada:**
```json
{
  "name": "Lab 104",
  "capacity": 0,
  "resources": []
}
```
**Resultado Esperado:** Status 422, mensagem "Capacidade deve ser maior que 0."

---

### CT13 – Criar sala com capacidade negativa
**Requisito:** RN05  
**Descrição:** Validar rejeição de capacidade negativa  
**Pré-condição:** ADMIN autenticado  
**Entrada:**
```json
{
  "name": "Lab 105",
  "capacity": -5,
  "resources": []
}
```
**Resultado Esperado:** Status 422, mensagem "Capacidade deve ser maior que 0."

---

### CT14 – Listar salas como USER
**Requisito:** RF05  
**Descrição:** Validar listagem de salas por USER  
**Pré-condição:** USER autenticado, salas cadastradas  
**Entrada:** GET /rooms (com token)  
**Resultado Esperado:** Status 200, lista de todas as salas

---

### CT15 – Listar salas como ADMIN
**Requisito:** RF05  
**Descrição:** Validar listagem de salas por ADMIN  
**Pré-condição:** ADMIN autenticado, salas cadastradas  
**Entrada:** GET /rooms (com token)  
**Resultado Esperado:** Status 200, lista de todas as salas

---

## Módulo 3: Reservas

### CT16 – Criar reserva válida
**Requisito:** RF06, RF08, RN06, RN07  
**Descrição:** Validar criação de reserva com dados válidos  
**Pré-condição:** USER autenticado, sala "Lab 101" existe  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "10:00",
  "end_time": "12:00",
  "purpose": "Aula de Algoritmos"
}
```
**Resultado Esperado:** Status 201, reserva criada com status CONFIRMED

---

### CT17 – Criar reserva com hora de início maior que término
**Requisito:** RN06  
**Descrição:** Validar rejeição de horário inválido  
**Pré-condição:** USER autenticado  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "15:00",
  "end_time": "14:00",
  "purpose": "Reunião"
}
```
**Resultado Esperado:** Status 422, mensagem "Hora de início deve ser menor que hora de término."

---

### CT18 – Criar reserva fora do horário permitido (antes das 08:00)
**Requisito:** RN07  
**Descrição:** Validar rejeição de horário antes das 08:00  
**Pré-condição:** USER autenticado  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "07:00",
  "end_time": "09:00",
  "purpose": "Estudo"
}
```
**Resultado Esperado:** Status 422, mensagem "Reservas permitidas apenas entre 08:00 e 22:00."

---

### CT19 – Criar reserva fora do horário permitido (após as 22:00)
**Requisito:** RN07  
**Descrição:** Validar rejeição de horário após 22:00  
**Pré-condição:** USER autenticado  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "21:00",
  "end_time": "23:00",
  "purpose": "Projeto"
}
```
**Resultado Esperado:** Status 422, mensagem "Reservas permitidas apenas entre 08:00 e 22:00."

---

### CT20 – Criar reserva com conflito de horário (sobreposição total)
**Requisito:** RN08  
**Descrição:** Validar detecção de conflito total  
**Pré-condição:** USER autenticado, reserva existente (10:00-12:00)  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "10:00",
  "end_time": "12:00",
  "purpose": "Outra atividade"
}
```
**Resultado Esperado:** Status 409, mensagem "Conflito de horário para esta sala."

---

### CT21 – Criar reserva com conflito de horário (sobreposição parcial - início)
**Requisito:** RN08  
**Descrição:** Validar detecção de conflito parcial no início  
**Pré-condição:** USER autenticado, reserva existente (10:00-12:00)  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "09:00",
  "end_time": "11:00",
  "purpose": "Atividade conflitante"
}
```
**Resultado Esperado:** Status 409, mensagem "Conflito de horário para esta sala."

---

### CT22 – Criar reserva com conflito de horário (sobreposição parcial - fim)
**Requisito:** RN08  
**Descrição:** Validar detecção de conflito parcial no fim  
**Pré-condição:** USER autenticado, reserva existente (10:00-12:00)  
**Entrada:**
```json
{
  "room_id": 1,
  "date": "2026-03-10",
  "start_time": "11:00",
  "end_time": "13:00",
  "purpose": "Atividade conflitante"
}
```
**Resultado Esperado:** Status 409, mensagem "Conflito de horário para esta sala."

---

### CT23 – Criar reserva com sala inexistente
**Requisito:** RN09  
**Descrição:** Validar rejeição de sala que não existe  
**Pré-condição:** USER autenticado  
**Entrada:**
```json
{
  "room_id": 999,
  "date": "2026-03-10",
  "start_time": "14:00",
  "end_time": "16:00",
  "purpose": "Teste"
}
```
**Resultado Esperado:** Status 404, mensagem "Sala não encontrada."

---

### CT24 – Criar reservas em salas diferentes no mesmo horário
**Requisito:** RN08  
**Descrição:** Validar que salas diferentes podem ter reservas simultâneas  
**Pré-condição:** USER autenticado, salas Lab 101 e Lab 102 existem  
**Entrada:**
```json
{
  "room_id": 2,
  "date": "2026-03-10",
  "start_time": "10:00",
  "end_time": "12:00",
  "purpose": "Aula em outra sala"
}
```
**Resultado Esperado:** Status 201, reserva criada (não há conflito)

---

### CT25 – Listar próprias reservas
**Requisito:** RF07  
**Descrição:** Validar listagem de reservas do usuário logado  
**Pré-condição:** USER autenticado com reservas criadas  
**Entrada:** GET /bookings/my (com token)  
**Resultado Esperado:** Status 200, lista apenas das reservas do usuário

---

### CT26 – Listar próprias reservas sem ter reservas
**Requisito:** RF07  
**Descrição:** Validar retorno de lista vazia  
**Pré-condição:** USER autenticado sem reservas  
**Entrada:** GET /bookings/my (com token)  
**Resultado Esperado:** Status 200, lista vazia

---

## Módulo 4: Incidentes

### CT27 – Criar incidente como USER
**Requisito:** RF09, RF11  
**Descrição:** Validar criação de incidente por USER  
**Pré-condição:** USER autenticado, sala existe  
**Entrada:**
```json
{
  "room_id": 1,
  "description": "Projetor não está funcionando corretamente"
}
```
**Resultado Esperado:** Status 201, incidente criado com status OPEN

---

### CT28 – Criar incidente como ADMIN
**Requisito:** RF09, RF11  
**Descrição:** Validar criação de incidente por ADMIN  
**Pré-condição:** ADMIN autenticado, sala existe  
**Entrada:**
```json
{
  "room_id": 1,
  "description": "Ar-condicionado não liga, necessário reparo"
}
```
**Resultado Esperado:** Status 201, incidente criado com status OPEN

---

### CT29 – Criar incidente com descrição curta
**Requisito:** RN10  
**Descrição:** Validar rejeição de descrição com menos de 10 caracteres  
**Pré-condição:** USER autenticado  
**Entrada:**
```json
{
  "room_id": 1,
  "description": "Quebrado"
}
```
**Resultado Esperado:** Status 422, mensagem "Descrição deve ter no mínimo 10 caracteres."

---

### CT30 – Criar incidente com 10 caracteres (limite)
**Requisito:** RN10  
**Descrição:** Validar aceitação de descrição no limite mínimo  
**Pré-condição:** USER autenticado  
**Entrada:**
```json
{
  "room_id": 1,
  "description": "Luz quebra"
}
```
**Resultado Esperado:** Status 201, incidente criado

---

### CT31 – Fechar incidente como ADMIN
**Requisito:** RF10, RF12, RN11  
**Descrição:** Validar fechamento de incidente por ADMIN  
**Pré-condição:** ADMIN autenticado, incidente 1 com status OPEN  
**Entrada:** PATCH /incidents/1/close (com token ADMIN)  
**Resultado Esperado:** Status 200, incidente com status CLOSED

---

### CT32 – Fechar incidente como USER
**Requisito:** RN11  
**Descrição:** Validar bloqueio de fechamento por USER  
**Pré-condição:** USER autenticado, incidente 2 com status OPEN  
**Entrada:** PATCH /incidents/2/close (com token USER)  
**Resultado Esperado:** Status 403, mensagem "Acesso restrito a administradores."

---

### CT33 – Fechar incidente já fechado
**Requisito:** RN12  
**Descrição:** Validar rejeição de fechamento duplicado  
**Pré-condição:** ADMIN autenticado, incidente 1 com status CLOSED  
**Entrada:** PATCH /incidents/1/close (com token ADMIN)  
**Resultado Esperado:** Status 400, mensagem "Incidente já está fechado."

---

### CT34 – Fechar incidente inexistente
**Requisito:** RF10  
**Descrição:** Validar tratamento de incidente não encontrado  
**Pré-condição:** ADMIN autenticado  
**Entrada:** PATCH /incidents/999/close (com token ADMIN)  
**Resultado Esperado:** Status 404, mensagem "Incidente não encontrado."

---

## Resumo de Cobertura

| Módulo | Casos de Teste | RFs Cobertos | RNs Cobertas |
|--------|----------------|--------------|--------------|
| Autenticação | CT01-CT07 | RF01, RF02, RF03 | RN01, RN02, RN03 |
| Salas | CT08-CT15 | RF04, RF05 | RN03, RN04, RN05 |
| Reservas | CT16-CT26 | RF06, RF07, RF08 | RN06, RN07, RN08, RN09 |
| Incidentes | CT27-CT34 | RF09, RF10, RF11, RF12 | RN10, RN11, RN12 |
| **Total** | **34 casos** | **12 RFs** | **12 RNs** |

---

## Mapeamento de Endpoints

| Endpoint | Método | Casos de Teste Relacionados |
|----------|--------|----------------------------|
| `/auth/register` | POST | CT01, CT02, CT03, CT04 |
| `/auth/login` | POST | CT05, CT06, CT07 |
| `/rooms` | POST | CT08, CT09, CT10, CT11, CT12, CT13 |
| `/rooms` | GET | CT14, CT15 |
| `/bookings` | POST | CT16, CT17, CT18, CT19, CT20, CT21, CT22, CT23, CT24 |
| `/bookings/my` | GET | CT25, CT26 |
| `/incidents` | POST | CT27, CT28, CT29, CT30 |
| `/incidents/{id}/close` | PATCH | CT31, CT32, CT33, CT34 |

---

**Data de Criação:** 06/03/2026  
**Versão:** 1.0
