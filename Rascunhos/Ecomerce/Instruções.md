## Disciplina: Tecnologias de Front-End

## Curso: Análise e Desenvolvimento de Sistemas

## Turma: 2º ano

## Data de Entrega: 03/06

## Formato de Trabalho: Duplas

## Objetivo do Trabalho:

O desafio é criar um **catálogo de e-commerce**. Você usará a **API DummyJSON** para:

- Listar produtos.
    
- Visualizar detalhes de produtos.
    
- Navegar por categorias.
    
- Realizar buscas.
    
- (Opcional) Implementar um carrinho de compras.
    

A aplicação será feita com **Vue.js 3, Vite, Axios e TailwindCSS**. O objetivo é ver sua capacidade de construir uma interface interativa e bem feita, usando boas práticas.

## Descrição do Desafio:

Você deve desenvolver um front-end que consome a API e mostra os produtos como um catálogo, com as seguintes funcionalidades:

### Funcionalidades Principais:

1. **Listagem de Produtos:**
    
    - Mostrar todos os produtos, com nome, imagem, preço, categoria e estoque.
        
    - Organizar os produtos em um grid responsivo.
        
2. **Paginação:**
    
    - Os produtos devem ter paginação para navegar entre as páginas.
        
3. **Visualização de Detalhes do Produto:**
    
    - Ao clicar em um produto, ir para uma página com mais informações sobre ele.
        
4. **Menu de Categorias:**
    
    - Um menu (lateral ou superior) deve mostrar as categorias disponíveis.
        
    - Ao clicar em uma categoria, mostrar apenas os produtos dela.
        
5. **Busca de Produtos:**
    
    - Buscar produtos por nome. A busca deve ser em tempo real enquanto você digita.
        

### Desafio Extra (Opcional):

- **Ordenação de Produtos:**
    
    - Ordenar produtos por:
        
        - Preço (Crescente ou Decrescente)
            
        - Nome (A-Z ou Z-A)
            
    - Pode ser feito com um `select dropdown` ou botões.
        
- **Carrinho de Compras:**
    
    - Criar uma tela de carrinho para ver os produtos adicionados.
        
    - Alterar a quantidade de um produto ou removê-lo no carrinho.
        
    - Clicar em "Adicionar ao Carrinho" adiciona o produto com quantidade 1.
        
    - Alterar quantidade e remover só na tela do carrinho.
        

**Observação:** Não precisa de autenticação ou sessões. O carrinho deve ser persistente durante a navegação, mas não precisa ser salvo em banco de dados.

## Tecnologias Utilizadas:

- **Vue.js 3**
    
- **Vite** (como bundler)
    
- **Axios** (para consumir a API)
    
- **TailwindCSS** (para estilização)
    

## Critérios de Avaliação:

A avaliação será baseada em:

1. **Atendimento de Requisitos:**
    
    - A aplicação faz o que foi pedido nas funcionalidades principais.
        
    - Listagem, detalhes, categorias e busca funcionam bem.
        
    - Se fizer o desafio extra, o carrinho deve funcionar corretamente.
        
2. **Organização do Código:**
    
    - Código bem estruturado, modular e com componentes Vue reutilizáveis.
        
    - Boa organização de arquivos e pastas (ex: `components`, `views`, `services`).
        
3. **Boas Práticas de Programação:**
    
    - Código limpo, com comentários quando necessário, e fácil de entender.
        
    - Uso correto do Vue.js, seguindo padrões e reatividade.
        
    - Código sem repetições e fácil de manter.
        
4. **Separação de Componentes:**
    
    - Componentes divididos de forma clara e lógica (ex: grid de produtos, navegação, detalhes, carrinho).
        
    - Evitar componentes muito grandes; divida-os.
        
5. **Legibilidade:**
    
    - Código bem formatado e com estilo consistente.
        
    - Interface clara, intuitiva e fácil de usar.
        

## Recursos da API DummyJSON:

A API para usar é a [API DummyJSON](https://dummyjson.com/ "null"). A documentação mostra os endpoints para produtos, detalhes, categorias e busca.

## Requisitos de Layout:

- Use **TailwindCSS** para estilizar.
    
- O layout deve ser **responsivo** (funcionar em celular e desktop).
    
- O design deve ser **simples, mas organizado**, pensando na experiência do usuário.
    

## Instruções de Entrega:

1. **Repositório GitHub:**
    
    - O trabalho é em duplas e deve estar em um **repositório público no GitHub**.
        
    - Envie o link do repositório pelo Moodle para avaliação.
        
2. **README.md:**
    
    - O repositório deve ter um arquivo `README.md` com:
        
        - Descrição do projeto e funcionalidades.
            
        - Instruções para rodar a aplicação localmente (dependências, comandos).
            
        - Prints das telas (uma para cada funcionalidade principal).
            
        - Link para um vídeo no YouTube mostrando o app rodando. No vídeo, um da dupla deve explicar e demonstrar as funcionalidades.
            
3. **Vídeo no YouTube:**
    
    - Faça um vídeo curto (5-10 minutos) mostrando o projeto localmente.
        
    - Explique e demonstre as funcionalidades.
        
    - Faça o upload no YouTube e coloque o link no `README.md`.
        

## Data de Entrega:

- **Até 03/06.**
    

## Dúvidas e Suporte:

Se tiver dúvidas, pergunte nas aulas ou nos fóruns da plataforma. Boa sorte! Este desafio é para mostrar o que aprenderam.