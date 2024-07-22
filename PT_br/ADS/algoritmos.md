# Algaritmos

## O que são algaritmos

Algaritmos são passos a serem seguidos com o fim de se alcanlar algo. Nesse sentido, são muitas vezes comparados com receitas culinárias, no qual no final da receita terá um bolo.

### Principais elementos

- **Estado inicial e estado final(previsível)** - Para construção de um bom algoritmo é preciso ter um início bem determinado e um fim previsível (output) para saber sé tudo occore como esperado.
- **Passos sequenciais lógicos, precisos e finitos** - como exemplo, um algaritmo para atravesar a rua seria estruturado dessa forma:
  <ol>
    <li>olhar para os 2 lados da rua</li>
    <li>Verificar se o semáforo está verde</li>
    <li>andar</li>
    <li>repitir a ação de andar até chegar no outro lado da rua</li>
  </ol>
- **Produzir o fim desejado (output)** - No caso do exemplo acima, o fim desejado é atravesar a rua em segurança

### Construção de um algoritmo

Para construir um algoritmo, precisamos identificar e segui alguns passos:

<ol>
  <li>Coompreender o problema</li>
  <li>Identificar os dados de entrada</li>
  <li>Identificar os dados de saída</li>
  <li>
    Determinar quais são os passos necessários para transformar dados de entrada em informações de saída, observando regras e limitações
  </li>
  <li>Definir todos os passos a serem executados</li>
  <li>Construir o lagoritmo</li>
  <li>Testar o algoritmo</li>
  <li>Executar o algoritmo</li>
</ol>

#### **Exemplo**

algoritmo para calcular o volume de um reservatório, no qual pode ser no formato de paralelepípedo ou cilindro.

```Java
String format = formatoDoReservatorio;
double v;
if (format == "cilindro") {
  double r = raio;
  double h = altura;
  v = Math.PI * math.pow(r, 2) * h;
} else {
  double c = comprimento;
  double l = largura;
  double h = altura;
  v = h * l * c;
}
System.out.println("O volume do reservatório " + format + " são " + v + " L");
```

## Algoritmo _HASH_

<p><span style="color: #90EE90">Uma função de <i>hash</i> essencialmente transforma dados.</span> Suas principais aplicações são:</p>

- Busca de elementos em DB (data base)
- Verficação de integridade de dados grandes
- Armazenamento de senhas com segurança

As funções _hash_ permitem guardar dados sensíveis sem armazenar propriamente o dado. Podemos armazenar um senha, que ao ser cadastrada, salvamos o valor _hash_ dela. Nos acessos seguintes, ao informar a senha, iremos caluclar o _hash_ da senha digita e comparar com o _hash_ da senha armazenada previamente. Alguns dos modelos mais utilizados são **MD5** e a família **SHA**.
