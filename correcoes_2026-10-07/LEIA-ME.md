# Correção E2: descida do interruptor intermediário 43b (Circulação 2)

## Como aplicar no DWG `Cópia de Desenho3009GpCDH.dwg`
1. Abra o DWG e rode `SCRIPT` → `APAGAR_E2_intermediario_43b.scr`.
   O script apaga por handle 4 entidades do layer FIAÇÃO_COMERCIAL:
   - `1DC7A` e `1DC7B`: os 2 traços de retorno atuais;
   - `1DC7C`: o texto "2#1.5";
   - `1DC7D`: o texto "43b".
2. `INSERT` → `CORRECAO_E2_intermediario_43b.dxf`, com ponto de inserção `0,0`, escala 1 e "Explode" marcado (equivale a colar em `*0,0`).
   Isso insere 4 traços de retorno e os textos "43b" e "4#1.5", no layer FIAÇÃO_COMERCIAL, estilo Standard, altura 0,06.

## Verificação feita aqui
- Os handles do DWG, convertido pelo LibreDWG, são idênticos aos do DXF exportado pelo AutoCAD: 13.939 de 13.939.
- No desenho mesclado (original − 4 entidades + correção), o eletroduto `1DC79` passou a ter 4 retornos. A anotação "43b 4#1.5" fica a 0,006 m do próprio eletroduto e a 0,17 m do vizinho mais próximo, então não é ambígua.
