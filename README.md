# NeanderDivision

Programa para o simulador Neander que implementa a divisão por 2 e por 4 e a divisão entre dois valores sobre números inteiros positivos, representados em complemento de dois (ou seja, os operados estão na faixa entre 0 e 127, inclusive).

## Variáveis temporárias utilizadas e o endereço delas
137: A
140: -B(Quando for A/B) ou -2B(Quando for A/B*2)
144: Onde fica meu opcode temporário(já que faço as operações com A e só depois carrego o B)

## Valores fixos que usei para auxiliar nas operações e seus endereços
133: 255
135: 254(Usado no decremento para fazer a divisão por 2)
136: 252(Usado no decremento para fazer a divisão por 4)
138: 1
134: 0
141: 1(Usado para o erro de operando(s) negativo(s))
142: 2(Usado para o erro de código de operação inválido)
143: 4(Usado para o erro de tentativa de divisão por zero)

## Resumo
O programa primeiro carrega o valor de A e faz operações que tem só A(dependendo do que estiver no 130) e em seguida(se o opcode digitado tenha sido maior que 2) carrega o B
e faz os testes(ver se B é zero ou negativo) e faz as operações com ele(também dependendo do código), caso o opcode digitado não seja 1,2,3 ou 4, o programa mostra um erro de código inválido, o qual só foi possível devido às decrementações que foram feitas para testar os códigos de operação não tenham chegado a zero.
Nas divisões fiz um loop em que cada vez que a sequencia dentro dele era executada ele carregava o 132 e somava 1 para dar ir dando o resultado das divisões e também decrementava
do A: 2(A/2), 4(A/4), B(A/B) ou 2B(A/B*2), a cada decremento o programa salva o resultado num A temporário, o qual, dentro do loop, quando for zero 
ou negativo(aparece antes do teste para ver se foi zero, para no caso de o A ser ímpar e dar o resultado da divisão como sendo o maior inteiro) leva ao fim do programa

## Solução para overflow
O único modo de ocorrer overflow na representação nas divisões exigidas pelo trabalho é no caso 4, já que deve ser feito o B+B como sendo o denominador, caso a soma de B+B 
der um número maior que 255 então deu estouro e para a soma dar maior que 255 o B tem que ser maior em módulo do que 128(último negativo), então o programa faz uma verificação para ver se a soma de
B+B dá negativo, e caso isso for verdadeiro o complemento que seria feito a seguir dará positivo, acarretando em problemas para fazer a divisão por decremento de 2B, por isso que no 
programa se B+B der negativo ele dá um JMP para onde zera as variáveis temporárias e segue para o Halt.
