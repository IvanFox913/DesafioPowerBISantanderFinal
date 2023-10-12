# Desafio Processando e Transformando Dados com Power BI

### Descrição

Esse Desafio faz parte do Santander ***Bootcamp 2023 - Ciência de Dados com Python***

Como último desafio do módulo Visualização e Análise de Dados com Power BI iremos
utilizar uma coleção de dados provida para cumprir algumas tarefas. Essas tarefas
tem por objetivo exercitar os conceitos de análise e engenharia de dados além de
habilidades com a ferramenta Power BI.

### Objetivos

Os objetivos a serem cumpridos são:

* Integrar um banco de dados MySQL com o Power BI.
* Checar integridade dos dados providos, modificando ou retirando valores inconsistentes se necessário
> OBS: Se algum departamento não possuir gerente um deve ser atribuido a ele com dados ficticios.
* Modificar valores monetários para tipo Double Preciso.
* Verificar numero de horas dos projetos.
* Separar colunas complexas.
* Mesclar as colunas employee e department baseando-se na coluna employee.
* Realizar a junção dos colaboradores e respectivos nomes dos gerentes.
* Mesclar as colunas Nome e Sobrenome para ter apenas uma coluna definindo o nome dos colaboradores.
* Mesclar nomes de Departamente e Localização de modo a tornar cada departamento-local unicos.
* Explicar o por quê no caso acima só é permitido ser utilizada a mescla e não a atribuição.
* Agrupar colaboradores existem por gerente.
* Eliminar colunas desnecessárias ao relatório.

> Há um arquivo docx no repositório deste desafio com os objetivos tabralhados de forma mais detalhada.


### Passo a Passo

#### 1. Integração do banco de dados MySQL com o Power BI.

Primeiro os scripts de criação e população do banco são inseridos.
> Eles podem ser encontrados [aqui](https://github.com/julianazanelatto/power_bi_analyst/tree/main/M%C3%B3dulo%203/Desafio%20de%20Projeto).
> OBS: Esses scripts providos não estavam completamente aptos a criar o banco necessário.
> Uma correção deles foi disponibilizada pela [Giovanna Fantacini]https://github.com/giovannaFantacini/ e uma cópia estara disponivel nesse repositório.

Em seguida é feita a conexão do banco com o Power BI.

#### 2. Tratamento de dados inicial

Ao carregar os dados do banco MySQL utilizando o Power Query iremos realizar algumas transformações nos dados visando torna-los
mais apropriados para nossos futuros relatórios e dashboards.

* Uma verificação é realizada e todos os cabeçalhos parecem terem sido importados corretamente a partir do banco.
* Coluna Salary da tabela Employee é alterada para decimal fixo.
* Colunas desnecessárias são removidas.
* Foi feita uma verificação por valores nulos e o único encontrado parece se tratar do dono (ou alguem com cargo semelhante) da empresa.<br>Assim sendo ele terá seu superSSN alterado para referenciar a si mesmo, como maneira de garantir a integridade de dados.
* Um unico valor zero foi encontrado na tabela Works On na coluna Hours. Considerando que é possivel alguem ser atribuido a um projeto mas não ter iniciado o trabalho nele o valor será mantido.

#### 3. Adequações das tabelas

É requisitado que algumas tabelas tenham suas colunas unidas ou divididas com base nos objetivos. As seguintes alterações foram realizadas:

* O endereço na tabela Employee estava muito complexo, então ele foi dividido entre suas partes constituintes e elas renomeadas para melhor adequar a leitura.
* O numero do endereço foi alterado para tipo texto para melhor interpretaçao e evitar a possibilidade de calculo.
* Nome, nome do meio e sobrenome da tabela Employee foram concatenados em uma unica coluna.
* Tabela Employee e Department mescladas via inner join com as chaves Dno e Dnumber respectivamente. O nome do departamento foi mesclado a tabela Employee.
* Tabela Employee e Employee mescladas via inner join com as chaves super_ssn e ssn. O nome do Gerente foi adicionado a tabela Employee.
* Tabela Department e Dept_Locations mescladas e transformadas em nova tabela com as chaves Dnumber Dnumber. O nome da localização foi adicionado a tabela Department.
> As tabelas Department e Dept_Locations apenas podem ser mescladas devido ao problema de atribuição de valores das colunas já existentes as novas trazidas por uma adição.
> Assim a mescla garante a integridade dos dados já inseridos como uma atribuição dos dados novos trazidos pela tabela dept_locations que não eram antes contemplados na tabela Department.
* Uma View foi feita para focar na relação entre empregados e gerentes. A visualização de colunas foi ativa.
> Não consegui encontrar algum guia que ensinasse a como agrupar os empregados pelos gerentes, entretanto consegui faze-lo na visualização de matriz no relatório.

#### 4. Geração do relatório

Por fim devemos gerar um relatório contendo algumas informações requisitadas nos objetivos.

* Um design básico é feito para facilitar a visualização dos dados.
* Uma matriz foi adicionada contendo os gerentes e funcionarios. Eles estão agrupados por gerente. Isso foi feito desligando o Layout de nivel que se encontra no cabeçalho de linha > opções > layout de nivel. Também desliguei os icones para melhor visualização.
* Uma Tabela foi adicionada contendo as informações da nova tabela Department_Locations. Nela há o nome, Id e nome do gerente dos diferentes departamentos da empresa
* Um gráfico de barras foi adicionado descrevendo a quantidade de funcionários por departamento.
* Um gráfico de rosca foi adicionado contendo a quantidade de horas dedicada a cada projeto. Um card também foi adicionado citando a quantidade de horas totais disponibilizadas aos projetos.
* Um gráfico de pizza foi adicionado contendo a discrepancia entre homens e mulheres que trabalham na empresa.

#### 5. Conclusão

Enfim temos um relatório montado após a obtenção e tratamento dos dados. Assim completamos mais um desafio. Para maiores informações favor entrar em contato.
