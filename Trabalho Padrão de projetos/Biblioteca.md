Para aumentar a complexidade do projeto, podemos incluir funcionalidades adicionais e novas classes que abrangem mais aspectos de um sistema de gerenciamento de biblioteca. Vou incluir classes como `Funcionario`, `Reserva`, e `Notificacao`, além de métodos mais detalhados para gerenciar as operações.

### Componentes Adicionais e Relacionamentos
1. **Funcionario**
   - Atributos: `ID`, `Nome`, `Cargo`, `Salario`
   - Métodos: `RegistrarLivro()`, `GerenciarEmpréstimo()`, `EmitirNotificacao()`
   - Relacionamento: Associação com `Biblioteca` (funcionário trabalha na biblioteca)

2. **Reserva**
   - Atributos: `ID`, `DataReserva`, `StatusReserva`
   - Métodos: `EfetuarReserva()`, `CancelarReserva()`
   - Relacionamento: Associação com `Livro` e `Membro` (um membro pode reservar um livro)

3. **Notificacao**
   - Atributos: `ID`, `DataEnvio`, `Mensagem`
   - Métodos: `EnviarNotificacao()`
   - Relacionamento: Associação com `Membro` e `Funcionario` (notificação enviada por funcionário para o membro)

4. **Biblioteca** (atualizada)
   - Métodos adicionais: `RemoverLivro()`, `GerenciarReservas()`

### Diagrama de Classes UML Atualizado
```plaintext
+----------------+       +----------------+       +----------------+       +------------------+
|   Biblioteca   |<>---->|     Livro      |<>-----|   Empréstimo   |<------|      Membro      |
+----------------+       +----------------+       +----------------+       +------------------+
| Nome           |       | ISBN           |       | ID             |       | ID               |
| Endereço       |       | Título         |       | DataEmpréstimo |       | Nome             |
| ListaLivros    |       | Autor          |       | DataDevolução  |       | Endereço         |
| ListaMembros   |       | AnoPublicação  |       | Status         |       | Telefone         |
+----------------+       | Status         |       +----------------+       | Reservas[]        |
| AdicionarLivro()|      +----------------+       | RegistrarDevolução()| | RegistrarEmpréstimo()|
| RegistrarMembro()|     | AtualizarStatus()|     | CalcularMulta()     | | DevolverLivro()      |
| ListarLivros()   |     | ExibirDetalhes()|     +----------------+      | SolicitarReserva()    |
| RemoverLivro()   |     +----------------+                                  +------------------+
| GerenciarReservas()|                                                     
+----------------+                                                          
           |                                                                 
           |                                                                 
           |                                                                 
+----------------+         +----------------+       +----------------+       
|  Funcionario   |<>-------|    Reserva    |<----->|  Notificacao   |       
+----------------+         +----------------+       +----------------+       
| ID             |         | ID            |       | ID             |       
| Nome           |         | DataReserva   |       | DataEnvio      |       
| Cargo          |         | StatusReserva |       | Mensagem       |       
| Salario        |         +----------------+       +----------------+       
+----------------+         | EfetuarReserva()|     | EnviarNotificacao()|  
| RegistrarLivro()|        | CancelarReserva()|    +----------------+       
| GerenciarEmpréstimo()|   +----------------+                           
| EmitirNotificacao()  |                                                   
+----------------+                                                          
                       
```
### Explicação das Ligações Adicionadas
- **Associação** de `Funcionario` com `Biblioteca`, indicando que a biblioteca possui funcionários que a operam.
- **Associação** de `Reserva` com `Livro` e `Membro`, permitindo que um membro possa reservar um livro específico.
- **Associação** de `Notificacao` com `Funcionario` e `Membro`, representando o envio de notificações de funcionários para membros.

### Novos Cenários Suportados
1. **Gerenciamento de Reservas**: O sistema agora permite que membros reservem livros e recebam notificações sobre o status de suas reservas.
2. **Funcionários**: Os funcionários podem adicionar e remover livros, gerenciar empréstimos e enviar notificações.
3. **Notificações**: Notificações são enviadas para membros sobre atualizações, como devoluções pendentes ou reservas prontas.

Com essa estrutura, o sistema abrange funcionalidades de uma biblioteca real com maior detalhamento, oferecendo uma base sólida para a implementação em C#. Se precisar de ajuda na criação do código ou na representação visual da UML, estou à disposição!



Vou descrever os casos de uso para o sistema de **Gerenciamento de Biblioteca**. Cada caso de uso detalha uma funcionalidade específica e os atores envolvidos.

### Atores do Sistema
1. **Membro**: Usuário da biblioteca que pode emprestar, devolver e reservar livros.
2. **Funcionario**: Pessoa que gerencia a biblioteca, realiza operações administrativas e auxilia os membros.
3. **Sistema**: Entidade que automatiza as operações e interage com os usuários.

### Casos de Uso Principais
#### 1. Emprestar Livro
- **Ator Primário**: Membro
- **Descrição**: O membro solicita o empréstimo de um livro disponível.
- **Fluxo Principal**:
  1. O membro seleciona o livro desejado.
  2. O sistema verifica a disponibilidade do livro.
  3. O empréstimo é registrado e a data de devolução é gerada.
- **Fluxo Alternativo**:
  - Se o livro não está disponível, o sistema oferece a opção de reserva.

#### 2. Devolver Livro
- **Ator Primário**: Membro
- **Descrição**: O membro devolve um livro emprestado.
- **Fluxo Principal**:
  1. O membro apresenta o livro para devolução.
  2. O sistema registra a devolução e atualiza o status do livro.
  3. O sistema calcula e aplica multas, se houver atraso.
- **Fluxo Alternativo**:
  - Notificação é enviada em caso de multa.

#### 3. Reservar Livro
- **Ator Primário**: Membro
- **Descrição**: O membro reserva um livro indisponível.
- **Fluxo Principal**:
  1. O membro seleciona o livro que deseja reservar.
  2. O sistema registra a reserva e informa a data prevista de disponibilidade.
- **Fluxo Alternativo**:
  - Caso o membro já tenha reservas pendentes, o sistema não permite novas reservas.

#### 4. Gerenciar Livros
- **Ator Primário**: Funcionario
- **Descrição**: O funcionário adiciona, atualiza ou remove livros do acervo.
- **Fluxo Principal**:
  1. O funcionário acessa a seção de gerenciamento de livros.
  2. O sistema permite adicionar novos livros, editar informações ou remover livros do acervo.
- **Fluxo Alternativo**:
  - Se a remoção de um livro está relacionada a um empréstimo em andamento, o sistema impede a ação.

#### 5. Enviar Notificação
- **Ator Primário**: Funcionario
- **Descrição**: O funcionário envia notificações sobre devoluções pendentes, reservas prontas ou multas.
- **Fluxo Principal**:
  1. O funcionário seleciona o membro e a mensagem da notificação.
  2. O sistema envia a notificação por e-mail ou SMS.

#### 6. Registrar Novo Membro
- **Ator Primário**: Funcionario
- **Descrição**: O funcionário cadastra novos membros na biblioteca.
- **Fluxo Principal**:
  1. O funcionário coleta as informações pessoais do membro.
  2. O sistema registra o novo membro e gera um ID único.
- **Fluxo Alternativo**:
  - Se os dados do membro estiverem incompletos, o sistema solicita a correção.

### Diagrama de Casos de Uso (Representação Textual)
```plaintext
+------------------------------------+
|            Sistema                 |
|                                    |
|   [Emprestar Livro]                |
|   [Devolver Livro]                 |
|   [Reservar Livro]                 |
|   [Gerenciar Livros]               |
|   [Enviar Notificação]             |
|   [Registrar Novo Membro]          |
+------------------------------------+
       ^           ^         ^
       |           |         |
   +--------+   +--------+   +---------+
   | Membro |   | Funcionario |   Sistema  |
   +--------+   +------------+   (Interno) |
```

### Explicação dos Casos de Uso
- **Casos de uso principais** como `Emprestar Livro`, `Devolver Livro`, e `Reservar Livro` são executados pelos membros.
- **Casos de uso administrativos** como `Gerenciar Livros`, `Enviar Notificação`, e `Registrar Novo Membro` são realizados pelos funcionários.
- **O sistema** automatiza verificações, cálculos de multa, e envio de notificações.

Este caso de uso cobre os processos principais de uma biblioteca e ajuda a estruturar a lógica do sistema antes de partir para a implementação em C#. Se precisar de mais detalhes ou de um diagrama visual, posso ajudar!




Vou criar a estrutura das tabelas em SQL com base no diagrama de classes apresentado anteriormente. Essas tabelas serão normalizadas e incluirão os relacionamentos necessários entre elas.

### Tabelas e Relacionamentos em SQL

1. **Tabela `Biblioteca`**
```sql
CREATE TABLE Biblioteca (
    BibliotecaID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Endereco VARCHAR(255) NOT NULL
);
```

2. **Tabela `Livro`**
```sql
CREATE TABLE Livro (
    LivroID INT PRIMARY KEY AUTO_INCREMENT,
    ISBN VARCHAR(20) UNIQUE NOT NULL,
    Titulo VARCHAR(100) NOT NULL,
    Autor VARCHAR(100) NOT NULL,
    AnoPublicacao INT NOT NULL,
    Status ENUM('Disponível', 'Emprestado', 'Reservado') NOT NULL,
    BibliotecaID INT,
    FOREIGN KEY (BibliotecaID) REFERENCES Biblioteca(BibliotecaID)
);
```

3. **Tabela `Membro`**
```sql
CREATE TABLE Membro (
    MembroID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Endereco VARCHAR(255) NOT NULL,
    Telefone VARCHAR(15) NOT NULL,
    BibliotecaID INT,
    FOREIGN KEY (BibliotecaID) REFERENCES Biblioteca(BibliotecaID)
);
```

4. **Tabela `Funcionario`**
```sql
CREATE TABLE Funcionario (
    FuncionarioID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Cargo VARCHAR(50) NOT NULL,
    Salario DECIMAL(10, 2) NOT NULL,
    BibliotecaID INT,
    FOREIGN KEY (BibliotecaID) REFERENCES Biblioteca(BibliotecaID)
);
```

5. **Tabela `Empréstimo`**
```sql
CREATE TABLE Emprestimo (
    EmprestimoID INT PRIMARY KEY AUTO_INCREMENT,
    DataEmprestimo DATE NOT NULL,
    DataDevolucao DATE,
    Status ENUM('Em andamento', 'Concluído', 'Atrasado') NOT NULL,
    LivroID INT,
    MembroID INT,
    FOREIGN KEY (LivroID) REFERENCES Livro(LivroID),
    FOREIGN KEY (MembroID) REFERENCES Membro(MembroID)
);
```

6. **Tabela `Reserva`**
```sql
CREATE TABLE Reserva (
    ReservaID INT PRIMARY KEY AUTO_INCREMENT,
    DataReserva DATE NOT NULL,
    StatusReserva ENUM('Ativa', 'Cancelada', 'Concluída') NOT NULL,
    LivroID INT,
    MembroID INT,
    FOREIGN KEY (LivroID) REFERENCES Livro(LivroID),
    FOREIGN KEY (MembroID) REFERENCES Membro(MembroID)
);
```

7. **Tabela `Notificação`**
```sql
CREATE TABLE Notificacao (
    NotificacaoID INT PRIMARY KEY AUTO_INCREMENT,
    DataEnvio DATE NOT NULL,
    Mensagem VARCHAR(255) NOT NULL,
    FuncionarioID INT,
    MembroID INT,
    FOREIGN KEY (FuncionarioID) REFERENCES Funcionario(FuncionarioID),
    FOREIGN KEY (MembroID) REFERENCES Membro(MembroID)
);
```

### Relacionamentos Entre as Tabelas
- **`Livro`** tem uma chave estrangeira para `Biblioteca` para indicar em qual biblioteca o livro está localizado.
- **`Membro`** também tem uma chave estrangeira para `Biblioteca`, indicando a qual biblioteca o membro pertence.
- **`Funcionario`** é associado a uma `Biblioteca`, mostrando em qual local o funcionário trabalha.
- **`Emprestimo`** e **`Reserva`** têm chaves estrangeiras que referenciam `Livro` e `Membro`, representando as ações de empréstimo e reserva realizadas por membros.
- **`Notificacao`** está associada a `Funcionario` e `Membro`, mostrando quem enviou e quem recebeu as notificações.

### Explicação Adicional
- Os tipos de dados foram escolhidos de forma a garantir que informações importantes, como datas e valores, sejam representadas corretamente.
- Os relacionamentos `FOREIGN KEY` garantem a integridade referencial, impedindo operações que possam quebrar a lógica do banco de dados.
- Os `ENUM` são usados para limitar os valores dos status e garantir consistência nos dados.

Com essas definições, você tem a base de dados pronta para um sistema de gerenciamento de biblioteca com as funcionalidades descritas. Se precisar de ajuda com inserções de dados, consultas ou mais detalhes, posso fornecer!


