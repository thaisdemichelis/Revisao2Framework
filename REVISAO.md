# Revisão 2 - Fila de Impressão

Nome: Thaís De Michelis Silva
Turma: 3A1

## Correções realizadas

| Problema | Arquivo e método | Correção |
|---|---|---|
| DevicePreview | lib/main.dart, main e ImpressaoApp.build | App envolvido por DevicePreview, com locale e builder do DevicePreview no MaterialApp; botões do formulário em Wrap para não cortar em telas estreitas |
| Ordem de chegada | lib/repositories/impressao_repository.dart, listar | orderBy alterado de id DESC para id ASC |
| Quantidades válidas | lib/providers/impressao_provider.dart, validar | Condição alterada de < 0 para <= 0 |
| Consumo de papel | lib/providers/impressao_provider.dart, folhasDoDocumento | Cálculo alterado de paginas + copias para paginas * copias |
| Filtro Pendentes | lib/providers/impressao_provider.dart, _mostrar | Pendentes passa a mostrar impresso == 0 |
| Marcação individual | lib/repositories/impressao_repository.dart, alternarImpressao | Condição do update alterada de id <> ? para id = ? |

## Testes de conferência

| Teste | Resultado |
|---|---|
| Ordem da lista | Roteiro do evento, Cartaz da oficina, Lista de presença |
| Resumo | 3 documentos e 24 folhas |
| Folhas por documento | 12, 10 e 2 |
| Filtro Pendentes | Somente Roteiro do evento e Cartaz da oficina |
| Filtro Impressos | Somente Lista de presença |
| Zero páginas e zero cópias | Gravação recusada com mensagem, no cadastro e na edição |
| Marcar Roteiro como impresso | Somente o Roteiro é alterado |
| Recarregar a página | Marcação mantida |
| Cadastro, edição e exclusão | Funcionando |
| DevicePreview | Testado em 320 x 568 e 390 x 844 sem elementos cortados |

## Correção escolhida

Qual arquivo e método você alterou?

lib/repositories/impressao_repository.dart, método alternarImpressao.

Qual era a causa do problema?

O update usava a condição where 'id <> ?'. O operador <> significa "diferente de", então o comando alterava todos os documentos exceto o selecionado.

Como sua alteração resolveu o comportamento observado?

A condição passou a ser where 'id = ?'. Assim o update atinge somente o registro com o id do documento escolhido, que alterna entre impresso e pendente. Como a alteração é gravada no SQLite, a situação permanece após recarregar a página.
