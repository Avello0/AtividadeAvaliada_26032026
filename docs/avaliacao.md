# Avaliação — Engenharia de Software
**Sistema Integrado de Gestão de Farmácia — MVP Definido pelo Estudante**

Aluno: *João Victor Rocha Avello Correia*  
RA: *24001368*  
Data: *26/03/2026*  

---
# 1. Definição do MVP

Meu MVP cobre o processo de venda de produtos, desde a identificação/cadastro do cliente até a finalização da venda, incluindo:

Consulta de produtos
Verificação de estoque
Registro de venda
Atualização automática do estoque
Emissão de comprovante
Registro de contas a receber (para vendas a prazo)
✅ Dentro do MVP
Venda à vista e a prazo
Cadastro de cliente
Consulta de produtos
Controle de estoque básico
Geração de comprovante
Integração com contas a receber
❌ Fora do MVP
Gestão completa de fornecedores
Compras e contas a pagar
Relatórios avançados
Controle de múltiplas unidades
Sistema de permissões completo
🎯 Justificativa

Escolhi focar no processo de vendas por ser o núcleo do sistema, onde há maior impacto direto no negócio e maior integração entre funcionalidades.

---

# 2. Regras de Negócio (mínimo: 5)
RN01 — Venda condicionada ao estoque
Um produto só pode ser vendido se houver quantidade suficiente no estoque.

RN02 — Atualização automática de estoque
Toda venda deve reduzir automaticamente o estoque do produto.

RN03 — Cadastro obrigatório para venda a prazo
Clientes só podem comprar a prazo se estiverem cadastrados.

RN04 — Geração de conta a receber
Toda venda a prazo deve gerar automaticamente uma conta a receber.

RN05 — Emissão obrigatória de comprovante
Toda venda deve gerar um comprovante ao final.

RN06 — Validação de produto existente
O sistema deve impedir vendas de produtos não cadastrados.

---

# 3. Requisitos Funcionais

RF01 — Consultar produto
Permitir busca por nome, código ou fabricante.

RF02 — Verificar estoque
Exibir quantidade disponível do produto.

RF03 — Cadastrar cliente
Permitir cadastro rápido no momento da venda.

RF04 — Registrar venda
Permitir inserir produtos e quantidades.

RF05 — Calcular valor total
Somar automaticamente os itens da venda.

RF06 — Finalizar venda
Confirmar a venda e registrar no sistema.

RF07 — Atualizar estoque
Reduzir automaticamente após venda.

RF08 — Emitir comprovante
Gerar comprovante com detalhes da venda.

RF09 — Registrar venda a prazo
Criar conta a receber automaticamente.

RF10 — Consultar cliente
Buscar cliente já cadastrado.

---

# 🛡 4. Requisitos Não Funcionais

RNF01 — Desempenho
O sistema deve responder consultas em até 2 segundos.

RNF02 — Segurança
Apenas usuários autenticados podem acessar o sistema.

RNF03 — Usabilidade
Interface simples e intuitiva para atendentes.

RNF04 — Confiabilidade
O sistema não pode perder dados de vendas.

RNF05 — Disponibilidade
Sistema disponível durante horário comercial.

---

# 5. Casos de Uso
🎭 Atores
Atendente
Cliente
📌 Lista de Casos de Uso (10)
UC01 — Consultar Produto
UC02 — Verificar Estoque
UC03 — Cadastrar Cliente
UC04 — Consultar Cliente
UC05 — Registrar Venda
UC06 — Calcular Total
UC07 — Finalizar Venda
UC08 — Emitir Comprovante
UC09 — Registrar Venda a Prazo
UC10 — Atualizar Estoque
🔗 Relacionamentos (IMPORTANTE PRA NOTA)
✅ Includes (3 obrigatórios)
UC05 → include → UC01 (Consultar Produto)
UC05 → include → UC06 (Calcular Total)
UC07 → include → UC08 (Emitir Comprovante)
✅ Extends (3 obrigatórios)
UC03 → extend → UC05 (se cliente não existir)
UC09 → extend → UC07 (venda a prazo)
UC02 → extend → UC05 (verificação de estoque)
---

# 6. Documentação dos Casos de Uso
UC01 — Consultar Produto

Ator(es): Atendente
Descrição: Permite ao atendente buscar um produto no sistema por nome, código ou fabricante.
Pré-condições: Sistema ativo
Pós-condições: Produto exibido (caso encontrado)

Fluxo Principal
Atendente acessa a função de busca
Informa nome/código/fabricante
Sistema realiza busca
Sistema exibe resultado
Fluxos Alternativos / Exceções
FA01 — Produto não encontrado: Sistema informa que não há resultados
FA02 — Entrada inválida: Sistema solicita nova busca
Relacionamentos
Include: —
Extend: —
Diagrama de Atividade

flowchart TD
A[Início] --> B[Inserir dados do produto]
B --> C{Produto encontrado?}
C -->|Sim| D[Exibir produto]
C -->|Não| E[Exibir mensagem de erro]
D --> F[Fim]
E --> F

---

UC02 — Verificar Estoque

Ator(es): Sistema
Descrição: Verifica se há quantidade suficiente de um produto em estoque
Pré-condições: Produto selecionado
Pós-condições: Retorna disponibilidade

Fluxo Principal
Sistema recebe produto
Consulta estoque
Retorna quantidade disponível
Fluxos Alternativos
FA01 — Estoque zerado: Sistema informa indisponibilidade
Relacionamentos
Include: —
Extend: UC05
Diagrama

flowchart TD
A --> B[Consultar estoque]
B --> C{Quantidade > 0?}
C -->|Sim| D[Disponível]
C -->|Não| E[Indisponível]
D --> F[Fim]
E --> F

---

UC03 — Cadastrar Cliente

Ator(es): Atendente
Descrição: Permite cadastrar um novo cliente
Pré-condições: Cliente não cadastrado
Pós-condições: Cliente registrado

Fluxo Principal
Atendente inicia cadastro
Insere dados
Sistema valida
Sistema salva cliente
Fluxos Alternativos
FA01 — Dados inválidos: Solicitar correção
Relacionamentos
Include: —
Extend: UC05
Diagrama

flowchart TD
A --> B[Inserir dados]
B --> C{Dados válidos?}
C -->|Sim| D[Salvar cliente]
C -->|Não| E[Solicitar correção]
D --> F[Fim]
E --> B

---

UC04 — Consultar Cliente

Ator(es): Atendente
Descrição: Permite buscar cliente cadastrado
Pré-condições: Sistema ativo
Pós-condições: Dados do cliente exibidos

Fluxo Principal
Inserir identificação
Sistema busca cliente
Exibe dados
Fluxos Alternativos
FA01 — Cliente não encontrado
Relacionamentos
Include: —
Extend: —
Diagrama
flowchart TD
A --> B[Buscar cliente]
B --> C{Encontrado?}
C -->|Sim| D[Exibir dados]
C -->|Não| E[Erro]
D --> F[Fim]
E --> F


---

UC05 — Registrar Venda

Ator(es): Atendente
Descrição: Permite registrar itens de uma venda
Pré-condições: Sistema ativo
Pós-condições: Venda em andamento

Fluxo Principal
Iniciar venda
Consultar produto
Informar quantidade
Verificar estoque
Adicionar item
Calcular total
Fluxos Alternativos
FA01 — Produto inexistente
FA02 — Estoque insuficiente
Relacionamentos
Include: UC01, UC06
Extend: UC02
Diagrama
flowchart TD
A --> B[Consultar produto]
B --> C{Produto existe?}
C -->|Não| D[Erro]
C -->|Sim| E[Informar quantidade]
E --> F{Estoque suficiente?}
F -->|Não| G[Erro estoque]
F -->|Sim| H[Adicionar item]
H --> I[Calcular total]
I --> J[Fim]

---

UC06 — Calcular Total

Ator(es): Sistema
Descrição: Soma os valores da venda
Pré-condições: Itens adicionados
Pós-condições: Total calculado

Fluxo Principal
Receber itens
Somar valores
Exibir total
Diagrama
flowchart TD
A --> B[Somar valores]
B --> C[Exibir total]
C --> D[Fim]

---

UC07 — Finalizar Venda

Ator(es): Atendente
Descrição: Finaliza a venda
Pré-condições: Venda iniciada
Pós-condições: Venda registrada

Fluxo Principal
Confirmar venda
Registrar venda
Atualizar estoque
Emitir comprovante
Fluxos Alternativos
FA01 — Venda a prazo
Relacionamentos
Include: UC08
Extend: UC09
Diagrama
flowchart TD
A --> B[Confirmar venda]
B --> C{Venda a prazo?}
C -->|Sim| D[Registrar conta]
C -->|Não| E[Continuar]
D --> E
E --> F[Atualizar estoque]
F --> G[Emitir comprovante]
G --> H[Fim]


---

UC08 — Emitir Comprovante

Ator(es): Sistema
Descrição: Gera comprovante da venda

Fluxo Principal
Gerar dados
Emitir comprovante
Diagrama
flowchart TD
A --> B[Gerar comprovante]
B --> C[Fim]


---


UC09 — Registrar Venda a Prazo

Ator(es): Sistema
Descrição: Gera conta a receber

Fluxo Principal
Gerar conta
Definir vencimento
Salvar
Diagrama
flowchart TD
A --> B[Criar conta]
B --> C[Definir vencimento]
C --> D[Salvar]
D --> E[Fim]

---

UC10 — Atualizar Estoque

Ator(es): Sistema
Descrição: Atualiza estoque após venda

Fluxo Principal
Receber venda
Subtrair quantidade
Atualizar sistema
Diagrama
flowchart TD
A --> B[Receber venda]
B --> C[Atualizar estoque]
C --> D[Fim]


