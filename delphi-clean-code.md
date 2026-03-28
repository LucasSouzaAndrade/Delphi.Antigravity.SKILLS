---
name: delphi-clean-code
description: Skill obrigatória para escrever, refatorar e revisar código Delphi. Define as regras de arquitetura, formatação e nomenclatura (incluindo variáveis locais e estruturação) que devem ser rigorosamente seguidas.
---

# Padrões de Codificação Delphi e Código Limpo

Você atuará como um Engenheiro de Software Sênior escrevendo código Delphi. É estritamente obrigatório seguir as regras abaixo em qualquer trecho gerado ou modificado:

## 1. Nomenclatura e Variáveis
* **Variáveis Locais:** Devem iniciar obrigatoriamente com o prefixo **`L`** (Local), seguido de PascalCase.
    * *Exemplo:* `LDataInclusao`, `LUsuarioLogado`.
* **Parâmetros de Métodos:** Devem iniciar com o prefixo **`A`** (Argument), seguido de PascalCase.
    * *Exemplo:* `AIdUsuario`, `ANomeCompleto`.
* **Campos de Classe (Fields):** Devem iniciar com o prefixo **`F`** (Field), seguido de PascalCase.
    * *Exemplo:* `FConnection`, `FListaItens`.
* **Interfaces e Classes:**
    * Interfaces devem iniciar com **`I`** (ex: `IRepository`).
    * Classes devem iniciar com **`T`** (ex: `TServicePedido`).
* **Variáveis Globais:** São proibidas; deve-se utilizar `class var` como alternativa arquitetural.

## 2. Proibições Estritas
* **Sem Notação Húngara:** É proibido o uso de prefixos de tipo (como `sNome`, `iIdade`, `bAtivo`). O nome deve ser semântico.
* **Sem Underlines:** Não utilize underscores em nomes de variáveis (ex: `L_data_venda` está incorreto).
* **Sem Abreviações Obscuras:** Use nomes completos e claros. Use `Quantidade` em vez de `Qtd`, `Funcionario` em vez de `Func`.

## 3. Formatação e Indentação
* **Espaçamento:** A indentação deve ser configurada rigorosamente com 2 espaços.
* **Begin/End:** O comando `begin` deve sempre ter uma linha própria (nunca na mesma linha da condição) e o `end` correspondente deve estar alinhado a ele. A quebra de linha após o `begin` é mandatória.
* **Else:** O bloco `else` deve sempre ocupar uma linha isolada, nunca junto ao `end` do bloco anterior.
* **Cláusula Uses:** Declare apenas uma unit por linha para reduzir conflitos de merge e facilitar o controle de versão.

## 4. Comandos Proibidos e Restritos
* **Tipos Numéricos Obsoletos:** O tipo numérico `Real` é considerado obsoleto e deve ser substituído por `Double`. O uso de `Extended` é desencorajado por não ser otimizado para processadores modernos.

## 5. Estrutura de Classes, Métodos e Exceções
* **Tamanho e Coesão:** Os métodos devem ter idealmente entre 20 e 30 linhas, com apenas uma responsabilidade (SRP).
* **Parâmetros e ARC:** Utilize o modificador `const` para passagem de `string`, `record` e `array`. Nunca utilize `const` para instâncias de interfaces, pois isso quebra o controle de referência (ARC).
* **Tratamento de Exceções:** Blocos `try..except` nunca devem engolir os erros de forma silenciosa.
* **Gestão de Recursos:** Use `try..finally` para a limpeza de conexões e memória, obedecendo à regra de gerenciar estritamente um recurso por bloco.

## 6. Manipulação de Strings
* **Concatenação:** É obrigatório o uso da função `Concat()` para realizar a junção de strings. O uso do operador `+` para esta finalidade é proibido.
    * *Correto:* `LResultado := Concat(LPrefixo, LTexto, LSufixo);`
    * *Incorreto:* `LResultado := LPrefixo + LTexto + LSufixo;`

## 7. Instruções Finais para o Agente
1. Antes de entregar o Implementation Plan ou o código finalizado, faça uma revisão interna (silenciosa) validando se as regras de formatação (2 espaços), remoção de notação húngara e prefixos padronizados (`L`, `A`, `T`, `I`) foram plenamente respeitadas.
2. Revise todas as concatenações de string para garantir o uso de `Concat()`.
3. Garanta que nenhuma variável local (`var`) tenha sido criada sem o prefixo `L`.
4. Remova qualquer comentário que apenas descreva a linha de código subsequente.
5. Certifique-se de que a indentação está rigorosamente com 2 espaços.
6. Caso esteja modificando um arquivo legado e note violações que estejam no escopo de sua tarefa, realize a correção e aplique as diretrizes acima.

## 8. Limite de Linha e Quebras
* **Limite de 80 Colunas:** Nenhuma linha de código deve ultrapassar 80 caracteres.
* **Quebra de Linha (Continuation Indent):** Ao quebrar uma linha que ultrapassou o limite:
    * A linha de continuação deve ter uma indentação fixa de **1espaços** em relação ao início da linha anterior.
    * **Proibido:** Alinhar parâmetros ou sub-comandos verticalmente com parênteses ou operadores da linha superior.
    * *Correto:*
      ```delphi
      LTextoHistorico := Concat(FloatToStr(FValorAtual),
        ' ', FOperacao, ' ', edtDisplay.Text, ' = ');
      ```
    * *Incorreto:*
      ```delphi
      LTextoHistorico := Concat(FloatToStr(FValorAtual),
                                ' ', FOperacao, ' ', edtDisplay.Text, ' = ');
      ```