CT01 – Registrar usuário com dados válidos

Requisito: RF01
Descrição: Validar registro com dados corretos.
Pré-condição: Email não cadastrado.
Entrada: Nome João Silva, Email joao@email.com
, Senha Senha123, Perfil USER.
Resultado Esperado: Usuário cadastrado com sucesso. HTTP 201 Created.

CT02 – Registrar usuário com email duplicado

Requisito: RN01
Descrição: Validar que email não pode ser repetido.
Pré-condição: Email já existente.
Entrada: Nome Maria, Email joao@email.com
, Senha Maria123, Perfil USER.
Resultado Esperado: Erro de duplicidade de email. HTTP 400 Bad Request.

CT03 – Registrar usuário com senha inválida

Requisito: RN02
Descrição: Validar regra mínima de senha.
Pré-condição: Nenhuma.
Entrada: Nome Carlos, Email carlos@email.com
, Senha abcdefg, Perfil USER.
Resultado Esperado: Erro de validação de senha (mínimo 8 caracteres, 1 letra e 1 número). HTTP 400 Bad Request.

CT04 – Login com credenciais válidas

Requisito: RF02, RF03
Descrição: Validar autenticação correta.
Pré-condição: Usuário previamente cadastrado.
Entrada: Email joao@email.com
, Senha Senha123.
Resultado Esperado: Retornar token válido. HTTP 200 OK.

CT05 – Login com senha incorreta

Requisito: RF02
Descrição: Validar erro de autenticação.
Pré-condição: Usuário existente.
Entrada: Email joao@email.com
, Senha Errada123.
Resultado Esperado: Credenciais inválidas. HTTP 401 Unauthorized.

CT06 – Acesso sem token

Requisito: RN03
Descrição: Validar obrigatoriedade de autenticação.
Pré-condição: Nenhuma.
Entrada: GET /rooms sem header Authorization.
Resultado Esperado: Acesso negado por ausência de token. HTTP 401 Unauthorized.

CT07 – ADMIN criar sala válida

Requisito: RF04
Descrição: Validar criação de sala por ADMIN.
Pré-condição: ADMIN autenticado.
Entrada: Nome Lab 01, Capacidade 30, Recursos Projetor.
Resultado Esperado: Sala criada com sucesso. HTTP 201 Created.

CT08 – USER tentar criar sala

Requisito: Permissões de Acesso
Descrição: Validar restrição de criação de sala para perfil USER.
Pré-condição: USER autenticado.
Entrada: POST /rooms.
Resultado Esperado: Acesso proibido para o perfil USER. HTTP 403 Forbidden.

CT09 – Criar sala com nome duplicado

Requisito: RN04
Descrição: Validar que não pode repetir nome da sala.
Pré-condição: Sala “Lab 01” já cadastrada.
Entrada: Nome Lab 01, Capacidade 20.
Resultado Esperado: Erro de duplicidade de nome. HTTP 400 Bad Request.

CT10 – Criar sala com capacidade inválida

Requisito: RN05
Descrição: Validar que a capacidade deve ser maior que zero.
Pré-condição: ADMIN autenticado.
Entrada: Nome Lab 02, Capacidade 0.
Resultado Esperado: Erro de validação de capacidade. HTTP 400 Bad Request.

CT11 – Listar salas autenticado

Requisito: RF05
Descrição: Validar listagem de salas cadastradas.
Pré-condição: Usuário autenticado.
Entrada: GET /rooms.
Resultado Esperado: Lista de salas retornada com sucesso. HTTP 200 OK.

CT12 – Criar reserva válida

Requisito: RF06, RF08
Descrição: Validar criação de reserva sem conflito e dentro do horário permitido.
Pré-condição: Sala existente e disponível.
Entrada: ID Sala 1, Data 2026-03-10, Hora 10:00–12:00, Finalidade Aula prática.
Resultado Esperado: Reserva criada com status CONFIRMED. HTTP 201 Created.

CT13 – Hora início maior que término

Requisito: RN06
Descrição: Validar que hora de início deve ser menor que hora de término.
Pré-condição: Sala existente.
Entrada: Hora 14:00–12:00.
Resultado Esperado: Erro de validação de horário. HTTP 400 Bad Request.

CT14 – Reserva fora do horário permitido

Requisito: RN07
Descrição: Validar funcionamento entre 08:00 e 22:00.
Pré-condição: Sala existente.
Entrada: Hora 07:00–09:00.
Resultado Esperado: Erro de horário inválido. HTTP 400 Bad Request.

CT15 – Conflito de horário

Requisito: RN08
Descrição: Validar interseção de horários na mesma sala e data.
Pré-condição: Reserva existente 10:00–12:00 na mesma sala e data.
Entrada: Hora 11:00–13:00.
Resultado Esperado: Conflito de horário detectado. HTTP 409 Conflict.

CT16 – Reserva para sala inexistente

Requisito: RN09
Descrição: Validar existência da sala antes da criação da reserva.
Pré-condição: Sala ID 999 inexistente.
Entrada: ID Sala 999.
Resultado Esperado: Sala não encontrada. HTTP 404 Not Found.

CT17 – Listar próprias reservas

Requisito: RF07
Descrição: Validar retorno apenas das reservas do usuário autenticado.
Pré-condição: Usuário com reservas cadastradas.
Entrada: GET /bookings/my.
Resultado Esperado: Lista contendo apenas reservas do usuário logado. HTTP 200 OK.

CT18 – Abrir incidente válido

Requisito: RF09, RF11
Descrição: Validar abertura de incidente para sala existente.
Pré-condição: Sala existente.
Entrada: ID Sala 1, Descrição com mais de 10 caracteres.
Resultado Esperado: Incidente criado com status OPEN. HTTP 201 Created.

CT19 – Abrir incidente com descrição curta

Requisito: RN10
Descrição: Validar tamanho mínimo da descrição do incidente.
Pré-condição: Sala existente.
Entrada: Descrição “Quebrou”.
Resultado Esperado: Erro de validação de descrição. HTTP 400 Bad Request.

CT20 – USER tentar fechar incidente

Requisito: RN11
Descrição: Validar permissão para encerramento de incidente.
Pré-condição: Incidente OPEN, usuário USER autenticado.
Entrada: PATCH /incidents/1/close.
Resultado Esperado: Acesso proibido para perfil USER. HTTP 403 Forbidden.

CT21 – ADMIN fechar incidente aberto

Requisito: RF10, RN12
Descrição: Validar encerramento correto de incidente aberto.
Pré-condição: Incidente OPEN, ADMIN autenticado.
Entrada: PATCH /incidents/1/close.
Resultado Esperado: Status alterado para CLOSED com sucesso. HTTP 200 OK.

CT22 – Fechar incidente já fechado

Requisito: RN12
Descrição: Validar que não é possível finalizar incidente já encerrado.
Pré-condição: Incidente com status CLOSED.
Entrada: PATCH /incidents/1/close.
Resultado Esperado: Conflito de estado do recurso. HTTP 409 Conflict.

CT23 – Token inválido

Requisito: Regras de Autenticação
Descrição: Validar token malformado ou inválido.
Pré-condição: Nenhuma.
Entrada: Authorization: Bearer token_invalido.
Resultado Esperado: Token inválido. HTTP 401 Unauthorized.

CT24 – Token expirado

Requisito: Regras de Autenticação
Descrição: Validar uso de token expirado.
Pré-condição: Token expirado.
Entrada: Requisição autenticada com token expirado.
Resultado Esperado: Token expirado. HTTP 401 Unauthorized.
