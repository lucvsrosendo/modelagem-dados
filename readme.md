# Desafio de Projeto: Refinando um Projeto Conceitual de Banco de Dados – E-commerce

Este repositório contém a resolução do desafio de modelagem de banco de dados proposto no bootcamp. O objetivo principal foi refinar o esquema conceitual de um e-commerce, aplicando melhorias nas estruturas de Clientes, Pagamentos e Entregas.

### 🛠️ Implementações Realizadas:

* **Cliente PJ e PF:** Foi utilizada a abordagem de especialização/generalização. Criamos uma entidade genérica `Cliente` que contém os dados comuns, ramificando para `Cliente_PF` (com CPF) e `Cliente_PJ` (com CNPJ). Isso garante que uma conta seja física ou jurídica, de forma exclusiva.
* **Múltiplas Formas de Pagamento:** Foi criada a entidade `Forma_Pagamento` com relacionamento de 1:N com a entidade `Cliente`. Isso permite que um mesmo usuário cadastre diferentes métodos de pagamento.
* **Gestão de Entregas:** A entidade `Entrega` foi criada e associada diretamente à entidade `Pedido` (relacionamento 1:1). Nela, foram inseridos os atributos `status_entrega` e `codigo_rastreio`, garantindo o acompanhamento logístico de cada compra.

### 📊 Diagrama de Entidade-Relacionamento (DER)

Abaixo está o modelo conceitual desenvolvido:

erDiagram
    Cliente {
        int id_cliente PK
        string nome
        string endereco
        string telefone
        string email
    }
    
    Cliente_PF {
        int id_cliente PK
        string cpf
    }
    
    Cliente_PJ {
        int id_cliente PK
        string cnpj
        string razao_social
    }
    
    Forma_Pagamento {
        int id_pagamento PK
        int id_cliente FK
        string tipo_pagamento
        string dados_pagamento
    }
    
    Pedido {
        int id_pedido PK
        int id_cliente FK
        date data_pedido
        float valor_total
    }
    
    Entrega {
        int id_entrega PK
        int id_pedido FK
        string status_entrega
        string codigo_rastreio
    }

    Cliente ||--o| Cliente_PF : "e um PF"
    Cliente ||--o| Cliente_PJ : "e um PJ"
    Cliente ||--|{ Forma_Pagamento : "cadastra"
    Cliente ||--|{ Pedido : "realiza"
    Pedido ||--|| Entrega : "gera"
