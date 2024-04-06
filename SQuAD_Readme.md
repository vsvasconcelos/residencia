# Dataset Card para SQuAD v1.1 em Português

<h2 style='text-align: center;'> Time 1 - NLP </h2>



## Dados Gerais

<!-- Se você está apenas usando um dataset já existente, coloque aqui os dados
do dataset original. Se você está combinando ou alterando datasets, ou está
construindo um dataset novo, preencha apenas o nome do dataset. -->

- **Nome:** SQuAD-pt_BR-V1.1
- **Página WEB:** [SQuAD-pt_BR-V1.1](https://huggingface.co/datasets/vsvasconcelos/SQuAD-pt_BR-V1.1_)
- **Repositório:** [SQuAD-pt_BR-V1.1 - /tree/main](https://huggingface.co/datasets/vsvasconcelos/SQuAD-pt_BR-V1.1_/tree/main)
- **Artigo:** [Question Answering on the SQuAD Dataset](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/reports/2761899.pdf)
- **Licença:** [MIT](https://choosealicense.com/licenses/mit/)

## Resumo

<!-- Elabore uma breve descrição do dataset, informando: 
* Se foram usados datasets já existentes (quais são esses datasets?).
* O uso principal pretendido (classificação de texto, reconhecimento de entidades, etc.).
* Os principais idiomas presentes.
* O domínio dos dados. -->

O conjunto de dados "Stanford Question Answering Dataset" (SQuAD), **para tarefa de perguntas e respostas extrativas**, foi desenvolvido em 2016. Utiliza perguntas geradas a partir de **536 artigos da Wikipedia** com cerca de 100.000 linhas de dados. Foi **construído** na forma de um **um contexto e uma pergunta** dos artigos da Wikipedia, onde **o contexto contém a resposta à pergunta**. [[1]](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/reports/2761899.pdf)     
Originalmente o SQuAD dataset foi construído no idioma inglês, contudo, o [grupo Deep Learning Brasil](http://www.deeplearningbrasil.com.br/) o traduziu automaticamente e fez ajustes manuais na tradução, gastando para isto cerca de 2 meses. [[2]](https://sol.sbc.org.br/index.php/kdmile/article/view/24974)    

Foi realizado uma [Análise Exploratória dos dados](https://nbviewer.org/github/vsvasconcelos/residencia/blob/main/EDA_squad_v1_pt.ipynb) dos arquivos disponibilizados pelo grupo Deep Learning Brasil, sendo eles:
> Conjunto de Treinamento: squad-train-v1.1.json (98MB); e     
> Conjunto de Validação: squad-dev-v1.1.json (16,5MB).     

Ambos arquivos foram disponibilizados no [gdrive](https://drive.google.com/file/d/1Q0IaIlv2h2BC468MwUFmUST0EyN7gNkn/view), pelo _grupo Deep Learning Brasil_ e ainda no repositório do dataset no [HuggingFace](https://huggingface.co/datasets/vsvasconcelos/SQuAD-pt_BR-V1.1_/blob/main/squad-pt.tar.gz), pelo _Time 1 de NLP_ da residência tecnológica do [CPQD](https://www.facebook.com/watch/?v=1131113184228595).


## Utilização Pretendida

<!-- Indique quais as tarefas de NLP podem utilizar este dataset. Por exemplo, 
classificação de texto, reconhecimento de entidades, etc. 
Nesta seção, você pode detalhar e expandir o que foi apresentado no resumo. -->

O SQuAD v1.1, se propõe à tarefas de perguntas e respostas extrativas.



## Idiomas

<!-- Indique os idiomas presentes no dataset. -->
A versão v1.1 do SQuAD foi traduzida automáticamente para a Lingua Portuguesa pelo grupo Deep Learning Brasil que depois disto fez ainda ajustes manuais adequando a tradução automática, gastando para isto cerca de 2 meses.



## Criação

<!-- Se o dataset foi construído por você, indique a fonte dos dados usados e
descreva o processo de coleta e processamento. Se foi usado um dataset já existente,
indique a URL do dataset original. Se o dataset existente foi modificado,
descreva a modificação realizada e as ferramentas usadas. -->  

Na [Análise Exploratória dos dados](https://nbviewer.org/github/vsvasconcelos/residencia/blob/main/EDA_squad_v1_pt.ipynb) realizada, verificou-se que os dois arquivos json, para treinamento e validação, possuem, respectivamente, 87.510 e 17.853 registros, totalizando assim: 105.363 dados.  
Foi constatado que os dados de testes não foram disponibilizados, e pesquisando em [[1]](https://web.stanford.edu/class/archive/cs/cs224n/cs224n.1174/reports/2761899.pdf), temos:   

> "[...] Utilizamos 80% do conjunto de dados para treinar o modelo, 10% para validação e ajuste hiperparâmetro. Os 10% finais do conjunto de dados são reservados para testes e mantidos privados pelos criadores da equipe com o objetivo de preservar a integridade dos modelos de resposta a perguntas."   

Portanto, os autores não disponibilizaram os 10% dos dados para testes. Sendo assim, desenvolvemos duas estratégias para contornar este problema:

* 1ª) Juntar os dados de treinamento e validação e depois redividi-los aleatoriamente em Treinamento (80%), Validação (10%) e Testes (10%);     
* 2ª) Manter os dados originais de treinamento e dividir o conjunto de validação em duas partes: validação (10 mil registros (9,5%) dos dados) e testes (7853 registros (7,4%) dos dados).  

Nas conversas com os mentores, acordamos que a 2ª estratégia é a melhor, pois possibilita melhores comparações com outras análises.   



## Estrutura

### Amostras

Os dois arquivos (squad-train-v1.1.json e squad-dev-v1.1.json) disponibilizados pelo grupo Deep Learning Brasil são estruturas de dados no formato [json](https://pt.wikipedia.org/wiki/JSON), conforme apresentado abaixo:

```json
{

"title": "Super_Bowl_50",    
"paragraphs":[
    {"context": "Super Bowl 50 was an American football game to ...",    
        {"question": "Where did Super Bowl 50 take place?",   
         "id": "56be4db0acb8001400a502ee",  
         "answers":[      
             {"answer_start": "403",   
              "text": "Santa Clara, California"}],
         ]},     
]}   
}
```
<!-- Se achar importante, dê informações adicionais sobre os dados e que não estejam
em outras seções, por exemplo, estatísticas sobre as amostras do dataset,
distribuição dos dados coletados, etc. -->


### Campos dos Dados

<!-- Indique e descreva os campos presentes no dataset. Informe o tipo do campo. 
Se for um campo de categoria, informe os valores possíveis. -->

* **title**: campo que trata de um determinado assunto/tema relacionado ao contexto.
* **context**: texto que contém a resposta para a questão.
* **question**: questão para ser respondida conforme o contexto.
* **Id**: identificador único da questão.
* **text**: resposta da questão conforme o contexto.
* **ans_start**: posição inicial da resposta à questão no campo contexto.


### Divisão dos Dados

<!-- Descreva as divisões existentes no dataset. Por exemplo, conjuntos de
treinamento, validação e teste. Forneça os tamanhos das divisões. Se achar
pertinente, forneça também estatísticas úteis de cada divisão. -->

Conforme apresentado anteriormente, acordamos em manter os dados originais de treinamento e dividir o conjunto de validação em duas partes: validação e testes. Contudo, quando começamos a comparar as versões 1.1 e 2.0 do SQuAD em inglês e português, descobrimos que a versão 1.1 pt, apesar de possuir 17.853 registros, destes somente 10.570 são registros únicos, isto é, no arquivo squad-dev-v1.1.json, muitas questões se repetiam muitas vezes com o mesmo 'Id'. Verificamos que na versão 1.1 us, temos realmente 10.570 registros, conforme  [[3]](https://arxiv.org/pdf/1806.03822.pdf).  
Desta forma, excluimos os registros duplicados - mantendo só os primeiros - do conjunto de validação da versão 1.1 pt importada por meio do arquivo squad-dev-v1.1.json.  
Assim, o conjunto de treinamento continuou com 87.510 e o de validação original passou de 17.853 registros para 10.570, totalizando 98.080 dados. O conjunto de treinamento permaneceu intacto, com 89,22% do total de dados, e o de validação foi dividido em validação, com 5.500 dados, 5,61%, e testes com 5.070 registros, equivamente a 5,17% do total de dados.  

Foram gerados 3 arquivos .csv, e carregados na plataforma [HungginFace](https://huggingface.co/datasets/vsvasconcelos/SQuAD-pt_BR-V1.1_/tree/main), sendo eles:
> squad_BR_train_.csv    
> squad_BR_valid_.csv    
> squad_BR_test_.csv    

Para carregar os datasets basta utilizar os seguintes comandos:

``` 
    # importar a biblioteca
    from datasets import load_dataset
    # carregar os datasets
    dataset = load_dataset("vsvasconcelos/SQuAD-pt_BR-V1.1_")
```
Que devem gerar a seguinte saída:

``` Saída comando
DatasetDict({
    train: Dataset({
        features: ['Id', 'title', 'context', 'question', 'ans_start', 'text'],
        num_rows: 87510
    })
    validation: Dataset({
        features: ['Id', 'title', 'context', 'question', 'ans_start', 'text'],
        num_rows: 5500
    })
    test: Dataset({
        features: ['Id', 'title', 'context', 'question', 'ans_start', 'text'],
        num_rows: 5070
    })
})
```



