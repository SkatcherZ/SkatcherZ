# Melhorias finais (rodada "para ficar 10")

Aplicar no DWG que você salvou **depois da CORRECAO_FINAL** (o save de 07/10, com 13.696 objetos). Conferi esse save aqui: é idêntico ao resultado esperado da CORRECAO_FINAL.

## Como aplicar
1. Abra uma **cópia** desse DWG e destrave todos os layers.
2. Rode `SCRIPT` → `APAGAR_MELHORIAS_FINAIS.scr`. A linha de comando deve mostrar
   `Apagados: 420 de 420. Nao encontrados: 0`.
   Se aparecer outro número, pare e me avise.
3. Rode `INSERT` → `MELHORIAS_FINAIS.dxf`, com ponto de inserção **digitado 0,0**, escala 1, rotação 0 e **Explode** marcado.
4. Rode `REGEN` e compare com `imagens/*_antes.png` e `imagens/*_depois.png`.
5. Entregue junto a planilha `Planilha Final - GRUPO 1 - 2026.2 (corrigida v2).xlsx`.

## O que muda

### 1. Circuito 29 (Subestação): TUG trifásica 3P+T 6000 VA
O slide de tomadas pede, na parte de tomadas trifásicas 3P+T, "no mínimo 1 tomada ≥ 6000 VA em subestação".

**Planilha**
| Aba / célula | Antes → Depois |
|---|---|
| Previsão G27 / I27 / J27 | 0 / "Exaustor / TUE" / 6000 → **1 TUG trifásica (6000 VA)** / – / – |
| Divisão A52, B52, F52, G52, I52 | 29 - TUE, 220 V, 1 fase, FP 1, J27/G52 → **29 - TUGs Trifásicas, 380 V, 3 fases, FP 0,8, ='Previsão'!H27** |
| Divisão L52–O52 | DTM 1P 32 A, IDR 2P 40 A → **DTM 3P 10 A, IDR 4P 25 A** |
| Capac. K52 / L52 | 2 / 10 → **3 / 2,5** |
| Queda E52 / F52 | 220 / 2 → **380 / 1,732** |
| Sobrecarga L52 | 57 → **21** (Iz de 2,5 mm², B1, 3 condutores) |
| Quadro de Cargas R56 | T → **R-S-T** |
| A52 em todas as abas | "29 - TUE" → "29 - TUGs Trifásicas" |

O resultado é IN = 9,12 A, seção final 2,5 mm² e Iz′ = 14,7 A ≥ 10 A.

Por que 10 A: com 16 A a regra Iz′ ≥ DTM não passa.

**Rebalanceamento do QD4:** com o 29 nas 3 fases, o 04 vai de R para T (R53) e o 37 de S para T (R59).
- Fases: R 36,4 / S 40,4 / T 38,8 A (desequilíbrio 5,5%).
- Testei todas as combinações de fase: este é o mínimo possível, por causa do circuito 28 (27,3 A monofásico).

**Planta**
- Nos 6 eletrodutos do 29, "29 2#10.0" virou "29 3#2.5", com 3 traços de fase.
- O PE passou a 1#2.5. Fica 1#10.0 só no trecho que também leva o 28.
- A tomada da Subestação ganhou o símbolo de tomada trifásica da legenda (triângulo dentro do círculo) e o texto "6000VA".

**Unifilar do QD4**
- Linha 29: RST, 3 fases antes do DTM, 3 polos, DTM 10 A, IDR 25 A, #2,5mm² e "29 - TUGS TRIFÁSICAS Subestação". Na coluna condutor: #2,5mm², Ø1.1/4".
- Fases: 04 → T, 37 → T.

### 2. Alimentador do QD1: 35 → 50 mm²
- QD1 e QD2 saem juntos do QGBT pelo mesmo leito. Com fator de agrupamento ≈ 0,88 (2 cabos multipolares):
  - 35 mm²: 126 × 0,88 ≈ 111 A, menor que o disjuntor de 125 A;
  - **50 mm²: 153 × 0,88 ≈ 135 A**, que atende.
- Planilha, Queda de Tensão: K60 = 50, N60 = 153, O60 = 25 (PE = S/2), com a explicação no texto de critérios (A65). ΔV fica em 1,2%. O QD2 passa: 238 × 0,88 ≈ 209 A ≥ 200 A.
- Unifilar do QD1: "4#50mm²", "Leito 4#50mm² + 1#25mm²" (×2) e os barramentos de neutro e terra com #50mm² e #25mm².

### 3. Legibilidade
- **Cotas:** as 116 cotas passaram de texto e seta 0,30 m para **0,15 m**. O valor de cada uma foi conferido: 116 de 116 com o mesmo texto de antes.
- **Nomes de ambiente:** 10 foram deslocados para pontos livres, sem atravessar paredes.
- **Etiquetas de máquina:** 8 deslocadas, sempre dentro do contorno do próprio motor ou bancada.
- **Etiquetas de luminária da fábrica:** 5 pares ("-xxa-" / "79,5") deslocados no máximo 0,35 m.
- **Anotações de fiação:** as de 16 eletrodutos comerciais que ficavam sob cotas foram reposicionadas. O conteúdo é idêntico, conferido 16 de 16.

| Medida | Antes | Depois |
|---|---|---|
| Textos de fiação comercial cobertos por outro texto | 34 | 6 |
| Textos de fiação da fábrica cobertos por outro texto | 39 | 7 |
| Textos de fiação cobertos por nome de ambiente ou etiqueta de máquina | 30 | 0 |
| Nomes de ambiente ou etiquetas de máquina sobre textos de luminária ou tomada | 10 | 0 |
| Sobreposições graves entre textos de fiação | 13 | 1 |

### 4. Não feito, por decisão sua
Caixa de passagem na saída do QD3/QD4. O slide diz "de preferência".

## Verificação feita aqui (sem AutoCAD)
- O resultado "DWG salvo − 420 + MELHORIAS_FINAIS.dxf" é idêntico, entidade a entidade, ao desenho validado: 13.697 objetos, sem nenhum objeto fora da área.
- Checagens no resultado:
  - 62 luminárias com circuito e retorno;
  - 20 interruptores;
  - 101 tomadas comerciais no circuito certo;
  - circuitos por eletroduto = "N° Circ. Agrup." da planilha em todos os circuitos;
  - todas as seções iguais à seção final;
  - nenhum eletroduto com mais de 8 condutores;
  - quantidade = traços em todos os eletrodutos refeitos;
  - 49 linhas de unifilar iguais à planilha (fase, DTM, IDR, seção e nº de fases antes do DTM).
- Planilha recalculada no LibreOffice, sem erros de fórmula: IN ≤ DTM ≤ Iz′ e IDR ≥ DTM em todos os circuitos; alimentadores com ΔV ≤ 2% e Iz ≥ disjuntor.

## Complemento (conferência do DesenhoFinal0710GpCDH)
Conferi o `DesenhoFinal0710GpCDH`, tanto o DWG quanto o DXF exportado pelo AutoCAD. Ele bate com o resultado esperado em 13.687 dos 13.697 objetos. Faltavam 10 objetos do layer LUMINOTÉCNICO na área de Tornear e Chanfrar/Polimento:
- as 6 cotas desse layer (com 0,15 m);
- 2 pares de etiquetas de luminária "-01a-" / "79,5".

Os originais desses objetos foram apagados pelo script, mas as versões novas não ficaram no desenho.

**Como completar:** `INSERT` → `COMPLEMENTO_LUMINOTECNICO.dxf`, digitando o ponto 0,0, escala 1 e Explode marcado. Não precisa de script, porque não há nada para apagar. Depois do insert, confira que essas 6 cotas e as 2 etiquetas aparecem na área de Tornear e Chanfrar.

Verificação: "DesenhoFinal0710GpCDH + COMPLEMENTO" é idêntico ao desenho validado (13.697 objetos, nenhuma diferença na comparação com tolerância de 0,01 m).
