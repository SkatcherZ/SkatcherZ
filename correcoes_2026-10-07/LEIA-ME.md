# Correções do projeto: Grupo 1, 2026.2

São dois pacotes independentes, ambos para o DWG **original** `Cópia de Desenho3009GpCDH.dwg`:

| Pacote | Arquivos | Conteúdo |
|---|---|---|
| **A. Correções gerais** | `APAGAR_CORRECOES_GERAIS.scr` + `CORRECOES_GERAIS.dxf` | Todas as correções desta revisão (lista abaixo) |
| **B. E2: intermediário 43b** | `APAGAR_E2_intermediario_43b.scr` + `CORRECAO_E2_intermediario_43b.dxf` | Descida 4#1.5 do intermediário 43b (Circulação 2) |

Os pacotes não se sobrepõem: nenhum handle aparece nos dois e nenhuma entidade é duplicada. Se você **já aplicou o B**, aplique só o A.

## Como aplicar (para cada pacote: primeiro o .scr, depois o .dxf)
1. Abra uma **cópia** do DWG original e destrave todos os layers (`LAYER` → Unlock all). O `entdel` não apaga objetos em layers travados.
2. `SCRIPT` → `APAGAR_CORRECOES_GERAIS.scr`. No fim, a linha de comando deve mostrar:
   `Apagados: 2153 de 2153. Nao encontrados: 0`
   Se aparecer outro número, o DWG não é o original. Pare e me avise.
3. `INSERT` → `CORRECOES_GERAIS.dxf`, com ponto de inserção `0,0`, escala 1, rotação 0 e **Explode** marcado. O resultado é o mesmo de colar em `*0,0`.
4. Para o pacote B, repita os passos 2 e 3 com os arquivos `*_E2_*`.
5. Rode `REGEN` e confira com as imagens em `imagens/` (`*_antes.png` / `*_depois.png`).

Os dois DXF estão em AutoCAD 2018 (AC1032), com unidade em metros e as mesmas layers e o mesmo estilo de texto (Standard) do desenho. As 5 cotas novas usam o dimstyle ISO-25 com as mesmas sobreposições das cotas originais (sufixo "m", vírgula decimal).

## O que o pacote A muda

### 1. Unifilares
- **DR "grudado" no circuito**: 20 MTEXT, em 10 linhas tri/bifásicas, foram afastados do texto do circuito.
- **Letras de fase**, conforme o novo balanceamento da planilha:
  06→T, 31→S, 33→R, 34→T (QD3); 04→R, 29→T, 35→S, 41→S (QD4).

### 2. Diretoria Técnica: luminotécnico
- A sala tinha 6 luminárias LHT44 (≈453 lx), abaixo dos 500 lx exigidos, e o método dos lúmens pede 7. Passou a ter **8 luminárias (2×4)**, com ≈604 lx.
- Os 13 eletrodutos e a fiação da sala foram redesenhados e 2 trechos foram acrescentados. As 4 cotas antigas deram lugar a 5 cotas novas, com espaçamento simétrico.

### 3. Saídas do QD3 e do QD4
- 14 eletrodutos de saída foram redesenhados em leque, sem cruzar uns com os outros, com as anotações de fiação reposicionadas.
- A topologia é a mesma: os mesmos circuitos e condutores, e os mesmos Ø (1", 1", 1.1/4").

### 4. Área comercial: anotações sobrepostas
- 113 eletrodutos tiveram as anotações de fiação reposicionadas. O conteúdo é idêntico: foi conferido eletroduto a eletroduto, 113 de 113.
- Textos de fiação com sobreposição grave: **241 → 13**.

### 5. Fábrica: "tripas" de circuitos
- Foram removidas 5 chamadas repetidas, que listavam de novo, no mesmo trecho de eletrocalha, circuitos já anotados:
  - (01, 12–15, 22, 23, 38, 39, 44–47)
  - (01, 12, 14, 15, 22, 23, 39, 44–47)
  - (14, 15, 23, 39)
  - (18, 19, 26, 40)
  - (02, 05, 17–21, 25–27, 40, 48, 49)
- Nas demais chamadas, as quantidades (n#seção) foram alternadas em altura para não se encavalarem.

## Planilha
`Planilha Final - GRUPO 1 - 2026.2 (corrigida).xlsx` é uma cópia; a original no Drive não foi alterada. Células de entrada alteradas:

| Aba | Célula | Antes → Depois | Motivo |
|---|---|---|---|
| Luminotécnico | AI22 | 3 → 4 | Diretoria: 2×4 luminárias |
| Capac.Cond.Corre. | F19 / G19 | 1 / 1 → 3 / 0,7 | Circuito 02: 3 circuitos no mesmo eletroduto |
| Quadro de Cargas | R41, R45, R47, R48 | S,R,T,S → T,S,R,T | Balanceamento do QD3 (06, 31, 33, 34) |
| Quadro de Cargas | R53, R56, R57, R60 | T,S,R,T → R,T,S,S | Balanceamento do QD4 (04, 29, 35, 41) |

Correntes por fase depois da mudança:
- QD3: 33,35 / 33,46 / 33,12 A.
- QD4: 38,18 / 38,22 / 39,09 A.

## Verificação feita aqui (sem AutoCAD)
- O resultado "original − 2153 handles + `CORRECOES_GERAIS.dxf` + pacote B" é idêntico, entidade a entidade, ao desenho final revisado: 13.727 entidades.
- Cada texto novo de fiação tem quantidade igual ao número de traços do seu eletroduto: 142 de 142.
- Ambiguidade texto↔eletroduto, ou seja, texto a menos de 3 cm de diferença entre o próprio eletroduto e o vizinho mais próximo: **24% nos textos novos contra 33% no desenho original**. Os casos restantes são feixes paralelos saindo de QD, onde os traços identificam o eletroduto.
- As cotas novas medem 0,97 / 1,93 / 1,93 / 1,93 / 0,97 m.
