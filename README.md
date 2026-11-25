# Integração de Dados: implantação, consultas e validação

**Disciplina:** Banco de Dados (ENGCO241M01)  
**Trabalho:** em equipe de até 5 pessoas  
**Prazo:** 19/11/2026

## Equipe

**Nome do time:** _______Gustavo_____________

| Nome | Matrícula | Usuário do GitHub |
| Gustavo Pantoja| 2408683| pantojagustavo63.coder


-- =====================================================
-- 1. QUANTIDADE DE REGISTROS POR TABELA
-- =====================================================

SELECT 'venda' AS tabela, COUNT(*) AS total
FROM venda

UNION ALL

SELECT 'pedido_compra', COUNT(*)
FROM pedido_compra

UNION ALL

SELECT 'entradas_mercadoria', COUNT(*)
FROM entradas_mercadoria

UNION ALL

SELECT 'produtos_filial', COUNT(*)
FROM produtos_filial

UNION ALL

SELECT 'fornecedor', COUNT(*)
FROM fornecedor;


-- =====================================================
-- 2. PEDIDOS COM ORDEM DE COMPRA ZERADA
-- =====================================================

SELECT *
FROM pedido_compra
WHERE ordem_compra = 0;


-- =====================================================
-- 3. PEDIDOS COM QUANTIDADE ENTREGUE MAIOR QUE A PEDIDA
-- =====================================================

SELECT *
FROM pedido_compra
WHERE qtde_entregue > qtde_pedida;


-- =====================================================
-- 4. ENTRADAS SEM PEDIDO CORRESPONDENTE
-- =====================================================

SELECT em.*
FROM entradas_mercadoria em
LEFT JOIN pedido_compra pc
    ON pc.ordem_compra = em.ordem_compra
    AND pc.produto_id = em.produto_id
WHERE pc.pedido_id IS NULL;


-- =====================================================
-- 5. PRODUTOS COM FORNECEDOR NÃO CADASTRADO
-- =====================================================

SELECT pf.*
FROM produtos_filial pf
LEFT JOIN fornecedor f
    ON f.idfornecedor = pf.idfornecedor
WHERE f.idfornecedor IS NULL;


-- =====================================================
-- 6. VENDAS DE FEVEREIRO DE 2025
-- =====================================================

SELECT
    COUNT(*) AS quantidade_lancamentos,
    SUM(qtde_vendida) AS unidades_vendidas,
    SUM(qtde_vendida * valor_unitario) AS faturamento
FROM venda
WHERE data_emissao >= DATE '2025-02-01'
  AND data_emissao < DATE '2025-03-01';
  
