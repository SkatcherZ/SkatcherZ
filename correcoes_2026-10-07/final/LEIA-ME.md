# Correção final, revisão do DWG entregue

Esta correção vale para o DWG que você enviou **depois** de aplicar as correções gerais e a E2, ou seja, o `Cópia de Desenho3009GpCDH.dwg` com 13.726 objetos.

## Como aplicar
1. Abra uma **cópia** desse DWG e destrave todos os layers (o `entdel` não apaga objetos em layer travado).
2. Rode `SCRIPT` → `APAGAR_CORRECAO_FINAL.scr`. A linha de comando deve mostrar
   `Apagados: 82 de 82. Nao encontrados: 0`.
   Se aparecer outro número, o DWG não é o enviado. Pare e me avise.
3. Rode `INSERT` → `CORRECAO_FINAL.dxf`, com ponto de inserção `0,0`, escala 1, rotação 0 e **Explode** marcado.
4. Rode `REGEN` e compare com `imagens/*_antes.png` e `imagens/*_depois.png`.

**Atenção ao ponto de inserção.** No DWG enviado havia uma segunda cópia da correção E2 (4 traços e os textos "43b" e "4#1.5") perto da origem 0,0, a cerca de 45 km do desenho. Ela foi inserida com outro ponto base. A cópia certa já está no lugar, e este script apaga a duplicada. Ao inserir este DXF, use o ponto **0,0** digitado, sem clicar na tela.

## O que muda (52 objetos novos, 82 apagados)

### 1. Unifilares: DR "grudado" (10 linhas tri/bifásicas)
O grupo de traços dos condutores ficava encostado e por dentro do retângulo do DR. Ele passou para depois do DR, na mesma posição das linhas monofásicas.

### 2. Unifilares: condutores iguais aos da planta e da planilha
| Linha | Antes | Depois | Base |
|---|---|---|---|
| 9 linhas RST (22, 23, 24, 25, 26, 27, 38, 39, 40) | N + 3F + PE | **3F + PE** | Na planta, as trifásicas estão como "3#…" + PE, sem neutro. Slide de tomadas: 3P+T 380/220 V. |
| RS: circuito 49, Bancada 6, bifásico | 3 fases antes do DTM, disjuntor com 3 polos, N + 3F + PE | **2 fases, 2 polos, 2F + PE** | Planilha: bifásico R-S com DTM 2P. Planta: "2#2.5" + PE. |

### 3. Rótulos de diâmetro nas saídas do QD3 e do QD4
Os 3 rótulos que recoloquei na correção anterior ficaram junto do eletroduto errado: os dois Ø1" no mesmo feixe e o Ø1.1/4" num trecho do circuito 41. Agora cada um fica junto do próprio eletroduto (a cerca de 0,10–0,16 m dele, com o vizinho a pelo menos 0,27 m):
- Ø1": QD3 → feixe 11/31/42;
- Ø1": QD3 → feixe 10/32/33;
- **Ø1.1/4": QD4 → 04/28/29**. Esse eletroduto leva cabos de 10 mm² e, em Ø3/4", ficaria com cerca de 52% de ocupação, acima de 40%.

### 4. Limpeza
- Removida a cópia duplicada da E2 perto da origem (6 objetos).
- Removida uma polilinha sem vértices no layer QUADROS (handle 208F4).

## Verificação feita aqui (sem AutoCAD)
- O DWG enviado (convertido pelo LibreDWG) e o DXF enviado têm os mesmos 13.726 handles.
- O resultado "DWG enviado − 82 + CORRECAO_FINAL.dxf" é idêntico, entidade a entidade, ao desenho revisado (13.696 objetos), e não sobra nenhum objeto fora da área do projeto.
- Checagens refeitas no resultado:
  - 62 luminárias comerciais com circuito e retorno;
  - 20 interruptores;
  - 101 tomadas comerciais no circuito certo;
  - 49 linhas de unifilar iguais à planilha (fase, DTM, IDR e seção).
