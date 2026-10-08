# Tarefa 2: dimensionamento dos CCMs (Grupo 1, 2026.2)

`Dimensionamento_CCM_Grupo1.xlsx` é uma cópia preenchida do modelo do professor (`Dimensionamento_CCM_-_2026.2_-_T2_4M12_5M34_1.xlsx`).

- **Todas as contas são fórmulas.** Isso inclui P, S, Q, IN, IP, IN′, seção por queda de tensão, IAJ, IF,min, fusível geral, demanda e FD.
- **São valores digitados só as escolhas:** dados de catálogo, seções comerciais, modelos e valores comerciais.
- O modelo não foi alterado na estrutura. Foram feitas só duas mudanças de mesclagem:
  - em Capac/Queda, as células B4:B11 foram mescladas, como já estavam os outros CCMs;
  - na Proteção, a mesclagem do disjuntor geral (AC/AD) foi corrigida para ficar por CCM. Antes estava em 6–14, 15–19 e 20–26.
- As notas e os critérios ficam na aba nova **"Notas Grupo 1"**.
- As imagens do modelo (equações e tabelas) foram preservadas: a planilha foi editada pelo LibreOffice e não pelo openpyxl.
- Recalculado no LibreOffice, **sem nenhum erro de fórmula**.

O desenho (Atividade 3) **não** foi mexido, como combinado.

---

## 1. Fontes usadas (Drive "Arquivos Professor")

| Arquivo | O que saiu dele |
|---|---|
| Slides – CCM | Fórmulas da Atividade 1, dados WEG W22 (slide 4) e regras da Atividade 2: FT = 1; ΔV ≤ 2,5%; motores no método E, PVC, Tab. 38; 75 HP e alimentadores no método F, EPR, Tab. 39; Tabela 42 (FA) |
| Aula 02 – Partida direta | IAJ = FS·IN; IF,min = 1,2·IAJ; TF > TP (TP = 5 s); IF ≤ IF,max; fusível geral; chave geral |
| Aula 03 – Estrela-triângulo / soft-starter | IAJ = FS·IN/√3; K1/K2 ≥ 1,15·IN/√3; K3 ≥ 0,33·IN·1,15; IF,min = 1,2·IAJ·√3; TF em IP/3; soft-starter (pesquisa no fabricante) |
| Aula 04 – Demandas | Fator de utilização, fator de simultaneidade, FD e "alimentador do CCM pela demanda" |
| SIEMENS_Reles_Contatores | Faixas dos relés 3RU11, contatores 3RT10 e fusível máximo **na combinação relé + contator** (coordenação tipo 2) |
| SIEMENS_Fusiveis_Diazed_NH | Curvas tempo × corrente, digitalizadas para obter o TF (ver `imagens/`) |
| Aula 01 – Condutores | Fórmula da ΔV e seção mínima |
| Planilha final da T1 (v2) | P, Q, corrente de projeto, L e disjuntores dos QD1–QD4 |
| DesenhoFinal0710GpCDH | Posição dos 24 motores, dos 4 CCMs, do QGBT e do leito existente |

---

## 2. Decisões tomadas (conferir com o grupo)

| # | Decisão | Por quê |
|---|---|---|
| 1 | **Circuitos 50 a 73** (M1…M24) | Continua a numeração única da T1 (01–49). O slide de exemplo mostra "01/02" nos motores de 75 cv. Se o professor quiser numeração por CCM, basta trocar a coluna A da Previsão. |
| 2 | **24 circuitos**, e não 22 | O slide fala em 22, mas a planilha e a planta do professor têm 24 motores. |
| 3 | **Partida:** até 10 HP direta; 15–40 HP estrela-triângulo; 75 HP soft-starter | É o que diz o modelo de unifilar do professor no DWG ("ATÉ 10 HP PARTIDA DIRETA / 10HP < x < 75 HP ESTRELA-TRIANGULO / 75 HP OU MAIS Soft-starter"). Também é coerente com as células I28:L28 mescladas só no 75 HP. A Aula 03 fala em soft-starter "a partir de 40 cv", o que diverge para os 40 HP. |
| 4 | **Dados dos motores:** tabela WEG W22 em HP (slide 4) | A planilha está em HP e tem a coluna FS. O PDF "dados motores" (em cv, FS 1,15) é o material antigo. |
| 5 | **Classes da demanda** pela potência nominal: 5–15 HP → "3 a 15 cv"; 20–40 → "20 a 40 cv"; 75 → "acima de 40 cv" | 15 HP = 15,2 cv e 40 HP = 40,6 cv caem nas bordas das classes. Segui o mesmo critério do unifilar do professor, que mistura HP e cv. |
| 6 | **FA dos motores:** Tab. 42 ref. 4 (eletrocalha perfurada), contando os cabos na saída de cada CCM (Y-Δ = 2 cabos) | CCM1 12 → 0,72; CCM2 8 → 0,72; CCM3 12 → 0,72; CCM4 2 → 0,88. |
| 7 | **FA dos alimentadores:** ref. 5 (leito), com 6 circuitos (QD1, QD2, CCM1–4) → 0,79 | O slide põe no leito os alimentadores "dos CCMs e QDs" que saem do QGBT. |
| 8 | **QD3 e QD4 continuam como na T1** (eletroduto embutido, método B1) | Eles não passam pela fábrica: o QD4 fica na área comercial. Na T1 constava "método E", mas o correto para eletroduto embutido é B1. Com B1 eles continuam passando (10 mm²: 50 A ≥ 50 A; 16 mm²: 68 A ≥ 63 A). |
| 9 | **QD1 e QD2 mudam:** EPR, método F, 35 mm² e 70 mm² | Com 6 circuitos no leito, os cabos PVC da T1 (50 e 95 mm²) já não atenderiam Iz′ ≥ disjuntor (153×0,79 = 121 < 125; 238×0,79 = 188 < 200). **Isso muda o unifilar e a planta da T1 na Atividade 3.** |
| 10 | **Comprimentos:** trajeto ortogonal medido na planta + subida/descida | CCM h = 1,60 m (igual aos QDs). Eletrocalha a 5,30 m e leito a 5,60 m: o pé-direito é 6 m e as luminárias ficam a 5 m. Caixa do motor a ≈ 0,50 m. **As alturas são hipótese de projeto.** |
| 11 | **ρ = 0,0178 e k = √3** | Mesmo critério da T1. |
| 12 | **Cabo do motor dimensionado por IN**, mais duas regras: mínimo de 2,5 mm² (circuito de força) e Iz′ ≥ ajuste do relé | No Y-Δ o relé mede a corrente de fase, então a regra Iz′ ≥ ajuste já fica satisfeita automaticamente. |

---

## 3. Resultados principais

### Motores (WEG W22, 380 V)
| HP | IN [A] | IP [A] | Partida | Relé (faixa) | Contator | Fusível | TF [s] | Seção |
|---|---|---|---|---|---|---|---|---|
| 5 | 8,21 | 68,2 | Direta | 3RU11 16-1KB0 (9–12) | 3RT10 17 | Diazed 20 A | ≈ 9 | 2,5 mm² |
| 7,5 | 11,96 | 87,3 | Direta | 3RU11 26-4AB0 (11–16) | 3RT10 25 | Diazed 25 A | ≈ 6,6 | 2,5 mm² |
| 10 | 14,65 | 120,1 | Direta | 3RU11 26-4BB0 (14–20) | 3RT10 26 | Diazed 35 A | ≈ 8,5 | 4 mm² |
| 15 | 22,14 | 183,8 (÷3 = 61,3) | Y-Δ | 3RU11 26-4AB0 (11–16) | K1/K2 3RT10 26 + K3 3RT10 23 | Diazed 35 A | ≈ 860 | 4 mm² |
| 20 | 30,05 | 270,5 (÷3 = 90,2) | Y-Δ | 3RU11 36-4DB0 (18–25) | K1/K2 3RT10 34 + K3 3RT10 24 | Diazed 50 A | ≈ 880 | 6 mm² |
| 30 | 44,60 | 356,8 (÷3 = 118,9) | Y-Δ | 3RU11 36-4FB0 (28–40) | K1/K2 3RT10 36 + K3 3RT10 25 | NH00 80 A | ≈ 2900 | 16 mm² |
| 40 | 57,10 | 399,7 (÷3 = 133,2) | Y-Δ | 3RU11 46-4HB0 (36–50) | K1/K2 3RT10 44 + K3 3RT10 26 | NH00 100 A | > 3000 | 16 mm² |
| 75 | 102,28 | 767,1 | Soft-starter | **A CONFIRMAR** | **A CONFIRMAR** | **A CONFIRMAR** | — | 35 mm² EPR |

**Por que alguns fusíveis ficaram acima do IF,min.** O fusível comercial logo acima do IF,min **não aguenta** os 5 s de partida:
- 5 HP com 16 A: ≈ 2 s;
- 7,5 HP com 20 A: ≈ 2,9 s;
- 10 HP com 25 A: ≈ 1,7 s.

Por isso subi um degrau em cada um. Todos ficam ≤ IF,max.

**Por que alguns contatores ficaram maiores que o mínimo.** Em vários Y-Δ, o contator mínimo daria um IF,max menor que o fusível necessário. É o mesmo raciocínio do exemplo da Aula 03 (15 cv → 3RT10 26).

### CCMs: demanda, fusível geral e alimentador
| CCM | P inst. [kW] | P dem. [kW] | FD | I dem. [A] | Fusível geral | Chave geral | Disjuntor no QGBT | Alimentador (EPR, F) | ΔV |
|---|---|---|---|---|---|---|---|---|---|
| CCM1 | 65,0 | 43,2 | 0,66 | 80,5 | NH00 160 A | 160 A | 100 A | 25 mm² | 1,16% |
| CCM2 | 79,9 | 53,8 | 0,67 | 99,5 | NH1 200 A | 200 A | 100 A | 25 mm² | 2,10% |
| CCM3 | 119,7 | 81,0 | 0,68 | 150,2 | NH2 300 A | 300 A | 160 A | 50 mm² | 1,01% |
| CCM4 | 117,1 | 91,7 | 0,78 | 160,2 | NH3 630 A* | 630 A* | 200 A | 70 mm² | 0,47% |
| **Total** | **381,9** | **269,8** | **0,71** | | | | | | |

\* Depende do fusível do 75 HP, que ainda está a confirmar.

---

## 4. Pendências e pontos de atenção

1. **Soft-starter do 75 HP: falta pesquisar o fabricante.**
   - É a atividade de pesquisa da Aula 03, e o catálogo não está no Drive.
   - O site da WEG e os espelhos do manual estão bloqueados na rede deste ambiente.
   - Deixei, marcados como **A CONFIRMAR**:
     - WEG **SSW07 0130** (130 A): o modelo existe e é de 130 A;
     - fusível aR **FNH1-400K-A**: vem de uma fonte secundária, **não conferi no manual**;
     - contator **3RT10 55** (150 A).
   - Ao confirmar no manual do SSW07 (tabela de fusíveis recomendados), basta trocar a célula R28/R29 da aba Proteção. O fusível geral do CCM4 se recalcula sozinho.
   - Com 400 A, o check "IF ≤ IF,max do contator (315 A)" não fecharia. Precisa ser revisto junto com o manual.
2. **Seletividade.** O fusível geral (regra da Aula 02: maior fusível + Σ IN) ficou **maior** que o disjuntor do QGBT em todos os CCMs. O disjuntor protege o alimentador (IB ≤ IDG ≤ Iz′), mas não há seletividade entre os dois. Vale perguntar ao professor se ele espera IDG ≥ IFG; nesse caso, os alimentadores ficam bem maiores.
3. **Alimentador do CCM2.** IB = 99,5 A com disjuntor de 100 A atende, mas fica no limite. A queda é de 2,10%. Somada à pior queda dos motores do CCM2 (0,54%), dá 2,64% do QGBT ao motor.
4. **Curvas de fusível.** Digitalizei as curvas Siemens do PDF (ver `imagens/`), com precisão de cerca de ± uma divisão secundária da escala logarítmica. Conferência com os exemplos das aulas:
   - 35 A @ 60,5 A: medi ≈ 940 s; a aula dá ≈ 1000 s.
   - 10 A @ 35 A: medi ≈ 6,4 s; a aula leu "10 s" a olho.
   - Todos os TF adotados têm folga grande sobre os 5 s, menos o 7,5 HP (≈ 6,6 s).
5. **Modelos de chave seccionadora e de disjuntor.** Não há catálogo deles no Drive. Por isso coloquei só a especificação ("seccionadora tripolar sob carga, X A, base NHx" e "disjuntor termomagnético tripolar, X A"), sem inventar código de produto.

## 5. Próximo passo (só depois de aprovar o Excel)
Atividade 3 no DWG:
- eletrocalhas dos CCMs acima dos perfilados;
- descidas em eletroduto rígido até cada motor;
- número do circuito em cada motor;
- fiação dos motores e dos alimentadores com as seções da planilha;
- atualização do QD1 e do QD2 (35 e 70 mm² EPR);
- unifilares dos CCMs.
