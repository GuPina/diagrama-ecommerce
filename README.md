CLIENTE
├── id_cliente (PK)
├── email (UNIQUE, NOT NULL)
├── senha_hash (NOT NULL)
├── nome_completo (NOT NULL)
├── cpf_cnpj (UNIQUE, NULLABLE)
├── telefone
├── data_nascimento
├── data_cadastro (TIMESTAMP, NOT NULL)
├── data_ultimo_acesso (TIMESTAMP)
├── status_cliente (ativo/inativo/bloqueado)
├── aceita_marketing (BOOLEAN, DEFAULT FALSE)
└── origem_cadastro (site/app/redes_sociais/indicacao)

ENDERECO
├── id_endereco (PK)
├── id_cliente (FK, NOT NULL)
├── tipo_endereco (entrega/cobranca/principal)
├── cep (NOT NULL)
├── logradouro (NOT NULL)
├── numero (NOT NULL)
├── complemento
├── bairro (NOT NULL)
├── cidade (NOT NULL)
├── uf (NOT NULL)
├── endereco_padrao (BOOLEAN, DEFAULT FALSE)
└── data_cadastro

CATEGORIA
├── id_categoria (PK)
├── nome_categoria (UNIQUE, NOT NULL)
├── slug_categoria (UNIQUE, NOT NULL)
├── id_categoria_pai (FK -> CATEGORIA, NULLABLE)
├── descricao_categoria
├── status_categoria (ativa/inativa)
├── ordem_exibicao (INTEGER)
└── data_criacao

PRODUTO
├── id_produto (PK)
├── sku (UNIQUE, NOT NULL)
├── nome_produto (NOT NULL)
├── slug_produto (UNIQUE, NOT NULL)
├── id_categoria (FK, NOT NULL)
├── descricao_curta (VARCHAR)
├── descricao_completa (TEXT)
├── preco_venda (DECIMAL, NOT NULL)
├── preco_promocional (DECIMAL, NULLABLE)
├── preco_custo (DECIMAL, NOT NULL)
├── peso_gramas (DECIMAL)
├── dimensoes_cm (VARCHAR)
├── estoque_atual (INTEGER, NOT NULL)
├── estoque_minimo (INTEGER, DEFAULT 5)
├── status_produto (ativo/inativo/esgotado)
├── destaque (BOOLEAN, DEFAULT FALSE)
├── visualizacoes (INTEGER, DEFAULT 0)
└── data_cadastro

PRODUTO_IMAGEM
├── id_imagem (PK)
├── id_produto (FK, NOT NULL)
├── url_imagem (NOT NULL)
├── alt_imagem (VARCHAR)
├── ordem_exibicao (INTEGER)
├── imagem_principal (BOOLEAN, DEFAULT FALSE)
└── data_upload

CARRINHO
├── id_carrinho (PK)
├── id_cliente (FK, NULLABLE)
├── session_id (VARCHAR, NULLABLE)
├── data_criacao (TIMESTAMP, NOT NULL)
├── data_ultima_atualizacao (TIMESTAMP)
├── status_carrinho (ativo/abandonado/convertido)
└── valor_total (DECIMAL, calculado)

CARRINHO_ITEM
├── id_carrinho_item (PK)
├── id_carrinho (FK, NOT NULL)
├── id_produto (FK, NOT NULL)
├── quantidade (INTEGER, NOT NULL)
├── preco_unitario_momento (DECIMAL, NOT NULL)
└── subtotal (DECIMAL, calculado)

PEDIDO
├── id_pedido (PK)
├── numero_pedido (UNIQUE, NOT NULL)
├── id_cliente (FK, NOT NULL)
├── id_endereco_entrega (FK, NOT NULL)
├── data_pedido (TIMESTAMP, NOT NULL)
├── status_pedido (pendente/confirmado/processando/enviado/entregue/cancelado/devolvido)
├── valor_produtos (DECIMAL, NOT NULL)
├── valor_frete (DECIMAL, NOT NULL)
├── valor_desconto (DECIMAL, DEFAULT 0)
├── valor_total (DECIMAL, NOT NULL)
├── forma_pagamento (cartao_credito/cartao_debito/pix/boleto/transferencia)
├── status_pagamento (pendente/aprovado/rejeitado/estornado)
├── origem_pedido (site/app/marketplace/telefone)
├── observacoes_cliente (TEXT)
└── data_ultima_atualizacao

PEDIDO_ITEM
├── id_pedido_item (PK)
├── id_pedido (FK, NOT NULL)
├── id_produto (FK, NOT NULL)
├── nome_produto_momento (VARCHAR, NOT NULL)
├── sku_momento (VARCHAR, NOT NULL)
├── quantidade (INTEGER, NOT NULL)
├── preco_unitario_momento (DECIMAL, NOT NULL)
└── subtotal (DECIMAL, calculado)

ENDERECO_ENTREGA
├── id_endereco_entrega (PK)
├── id_pedido (FK, NOT NULL)
├── nome_destinatario (NOT NULL)
├── telefone_destinatario
├── cep (NOT NULL)
├── logradouro (NOT NULL)
├── numero (NOT NULL)
├── complemento
├── bairro (NOT NULL)
├── cidade (NOT NULL)
├── uf (NOT NULL)
└── referencia

CUPOM_DESCONTO
├── id_cupom (PK)
├── codigo_cupom (UNIQUE, NOT NULL)
├── tipo_desconto (percentual/valor_fixo/frete_gratis)
├── valor_desconto (DECIMAL, NOT NULL)
├── valor_minimo_pedido (DECIMAL, DEFAULT 0)
├── data_inicio (DATE, NOT NULL)
├── data_fim (DATE, NOT NULL)
├── limite_uso_total (INTEGER, NULLABLE)
├── usos_realizados (INTEGER, DEFAULT 0)
├── status_cupom (ativo/inativo/esgotado)
└── data_criacao

ENVIO
├── id_envio (PK)
├── id_pedido (FK, NOT NULL)
├── transportadora (NOT NULL)
├── codigo_rastreamento (UNIQUE, NULLABLE)
├── prazo_entrega_dias (INTEGER)
├── data_postagem (DATE)
├── data_entrega_prevista (DATE)
├── data_entrega_real (DATE, NULLABLE)
├── status_envio (preparando/postado/transito/entregue/devolvido)
├── valor_frete (DECIMAL)
└── observacoes_envio

AVALIACAO_PRODUTO
├── id_avaliacao (PK)
├── id_produto (FK, NOT NULL)
├── id_cliente (FK, NOT NULL)
├── id_pedido (FK, NULLABLE)
├── nota (INTEGER, 1-5, NOT NULL)
├── titulo_avaliacao (VARCHAR)
├── comentario (TEXT)
├── data_avaliacao (TIMESTAMP, NOT NULL)
├── status_avaliacao (aprovada/pendente/rejeitada)
└── recomenda_produto (BOOLEAN)
