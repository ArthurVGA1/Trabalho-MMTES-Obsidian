### Passo a Passo para Criar o Diagrama

1. **Inicie a ferramenta de diagramação** (como Lucidchart, Draw.io, ou qualquer software UML).

2. **Crie as classes** usando retângulos. Para cada classe, você pode usar a seguinte estrutura:

   #### Produto
   ```
   +-----------------+
   |      Produto    |
   +-----------------+
   | - id: int       |
   | - nome: String  |
   | - descricao: String |
   | - quantidade: int |
   | - preco: float   |
   +-----------------+
   | + criarProduto() |
   | + lerProduto()   |
   | + atualizarProduto() |
   | + excluirProduto() |
   +-----------------+
   ```

   #### Categoria
   ```
   +-----------------+
   |    Categoria     |
   +-----------------+
   | - id: int       |
   | - nome: String  |
   | - descricao: String |
   +-----------------+
   | + criarCategoria() |
   | + lerCategoria()   |
   | + atualizarCategoria() |
   | + excluirCategoria() |
   +-----------------+
   ```

   #### Fornecedor
   ```
   +-----------------+
   |    Fornecedor    |
   +-----------------+
   | - id: int       |
   | - nome: String  |
   | - contato: String |
   +-----------------+
   | + criarFornecedor() |
   | + lerFornecedor()   |
   | + atualizarFornecedor() |
   | + excluirFornecedor() |
   +-----------------+
   ```

   #### Estoque
   ```
   +-----------------+
   |      Estoque     |
   +-----------------+
   | - produtos: List<Produto> |
   +-----------------+
   | + adicionarProduto() |
   | + removerProduto()   |
   | + listarProdutos()   |
   | + buscarProdutoPorId() |
   +-----------------+
   ```

3. **Adicione as relações**:
   - Desenhe uma linha entre **Produto** e **Categoria** para indicar a associação.
   - Desenhe uma linha entre **Produto** e **Fornecedor** para indicar a associação.
   - Desenhe uma linha com um losango preenchido do **Estoque** para **Produto** para indicar composição (um estoque contém produtos).

### Dicas

- Use setas para indicar a direção da relação se necessário.
- Mantenha o diagrama organizado e espaçado para fácil leitura.
- Certifique-se de que cada classe e suas relações sejam claramente visíveis.


As relações entre as tabelas (ou classes) do sistema de estoque podem ser descritas da seguinte forma:

### 1. **Produto e Categoria**
- **Relação:** Associação
- **Descrição:** Cada produto pertence a uma categoria. Uma categoria pode ter múltiplos produtos associados a ela.
- **Cardinalidade:** 
  - Um **Produto** está associado a uma única **Categoria**.
  - Uma **Categoria** pode ter muitos **Produtos**.

### 2. **Produto e Fornecedor**
- **Relação:** Associação
- **Descrição:** Cada produto pode ser fornecido por um ou mais fornecedores. Um fornecedor pode fornecer múltiplos produtos.
- **Cardinalidade:**
  - Um **Produto** pode ter múltiplos **Fornecedores**.
  - Um **Fornecedor** pode fornecer múltiplos **Produtos**.

### 3. **Estoque e Produto**
- **Relação:** Composição
- **Descrição:** O estoque contém uma coleção de produtos. Se o estoque for excluído, os produtos associados podem ser afetados.
- **Cardinalidade:**
  - Um **Estoque** contém múltiplos **Produtos**.
  - Um **Produto** deve estar em pelo menos um **Estoque**.

### Resumo das Relações

| Relação          | Entidades            | Tipo de Relação | Cardinalidade                     |
|------------------|----------------------|-----------------|-----------------------------------|
| Produto - Categoria | Produto e Categoria  | Associação      | 1 Produto : 1 Categoria, 1 Categoria : N Produtos |
| Produto - Fornecedor | Produto e Fornecedor | Associação      | N Produtos : N Fornecedores      |
| Estoque - Produto   | Estoque e Produto     | Composição      | 1 Estoque : N Produtos            |

Essas relações ajudam a modelar como os dados interagem entre si e são essenciais para o design do banco de dados. 