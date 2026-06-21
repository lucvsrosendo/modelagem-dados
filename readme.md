erDiagram
    Cliente {
        int id_cliente PK
        string nome
        string endereco
        string telefone
        string email
    }
    
    Cliente_PF {
        int id_cliente PK "FK"
        string cpf
    }
    
    Cliente_PJ {
        int id_cliente PK "FK"
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

    %% Relacionamentos
    Cliente ||--o| Cliente_PF : "é um (PF)"
    Cliente ||--o| Cliente_PJ : "é um (PJ)"
    Cliente ||--|{ Forma_Pagamento : "cadastra"
    Cliente ||--|{ Pedido : "realiza"
    Pedido ||--|| Entrega : "gera"