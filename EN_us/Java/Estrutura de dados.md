# Atribuição e Referência

- As atribuições em Java são por cópia de valor sempre; (tipos primitivos)
- Com tipo primitivo, copiamos o valor em memória;
- Com objetos copiamos o valor da referência em memória, sem duplicar o objeto.

# Conceito de Nó e Encadeamento de Nó (linked list)

É um espaço em memória que armazenda o dado desejado (_payload_) e uma referẽncia (_ponteiro_) para um próximo nó em memória.<br>
Para que possamos faz essa referência, temos que no alocar a referência do nó porsterior no nó atual, assim por diante. Quando cheagarmos ao último nó, a refreência dele será para `null`.

```Java
public class No {

    private String data;
    private No nextNo;

    public No(String data) {
        this.nextNo = null;
        this.data = data;
    }

    public String getData() {
        return data;
    }

    public No getNextNo() {
        return nextNo;
    }

    public void setData(String data) {
        this.data = data;
    }

    public void setNextNo(No nextNo) {
        this.nextNo = nextNo;
    }

    @Override
    public String toString() {
        return "No{" +
                "data='" + data + '\'' +
                ", nextNo=" + nextNo +
                '}';
    }
}

public class Main {
    public static void main(String[] args) {
        No no1 = new No("Conteúdo no1");
        No no2 = new No("Conteúdo no2");
        no1.setNextNo(no2);
        No no3 = new No("Conteúdo no3");
        no2.setNextNo(no3);
        No no4 = new No("Conteúdo no4");
        no3.setNextNo(no4);

        // no1 -> no2 -> no3 -> no4 -> null
        System.out.println("------------------");
        System.out.println(no1);
        System.out.println(no1.getNextNo());
        System.out.println(no1.getNextNo().getNextNo());
        System.out.println(no1.getNextNo().getNextNo().getNextNo());
        System.out.println(no1.getNextNo().getNextNo().getNextNo().getNextNo());
    }
}
```

# Generics

```Java
Lista<String> minhaLista = new Lista<>;

public class Lista<T> {
  private T t;
  //
}
```

Contexto:

- Evitar casting excessivo
- Evitar código redundantes
- Encontrar erros em tempo de compilação
- Introduzido desde o Java SE 5.0

## Wildcards (Coringa)

- Unknown Wildcards (Unbounded) _Ilimitado_
- Bounded Wildcard (Upper Bounded/Lower Bounded)

### Unknown Wildcard

```Java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {

        List<String> list = new ArrayList<>();
        list.add("a");
        list.add("b");
        list.add("c");
        list.add("d");
        System.out.println(list);
        printList(list);
        String[] a = {"A"};
        a.
    }

    public static void printList(List<?> list) {
        for (Object obj: list) {
            System.out.println(obj);
        }
    }
}
```

- Aqui a função `printList` pode imprimir lista de qualquer coisa, por conta do generics

### UpperBounded Wildcard

```Java
import java.util.ArrayList;
import java.util.List;

public class BoundedWildcard {
    public static void main(String[] args) {
        List<Aluno> myList = new ArrayList<Aluno>();
        printList(myList);
    }


    public static void printList(List<? extends Pessoa> listaPessoas) {
        for (Pessoa p : listaPessoas) {
            System.out.println(p);
        }
    }
}
```

- Nesse caso só consigo executar a função se a lista passada for da classe `Pessoa` ou extende-lá, no qual a class `Aluno` é filha da classe `Pessoa`.

### UpperBounded Wildcard

```Java
import java.util.ArrayList;
import java.util.List;

public class BoundedWildcard {
    public static void main(String[] args) {
        List<Aluno> myList = new ArrayList<Aluno>();
        printList(myList);
    }


    public static void printList(List<? super Pessoa> listaPessoas) {
        for (Pessoa p : listaPessoas) {
            System.out.println(p);
        }
    }
}
```

- Nesse caso só consigo executar a função se a lista passada for da classe `Pessoa`, outras listas ou alguma classe que `Pessoa` , não **aceitando nehum herdeiro** de `Pessoa`

### Convenção

- **K** para "Key", exemplo: Map<K,V>
- **V** para "Value", exemplo: Map<K,V>
- **E** para "Element", exemplo: List<E>
- **T** para "Type", exemplo: Collection#addAll
- **?** quando genérico

# Refatoração da Classe No para utlizar generics

```Java
public class No<T> {

    private T data;
    private No<T> nextNo = null;

    public No(T data) {
        this.data = data;
    }

    public T getData() {
        return data;
    }

    public No<T> getNextNo() {
        return nextNo;
    }

    public void setData(T data) {
        this.data = data;
    }

    public void setNextNo(No nextNo) {
        this.nextNo = nextNo;
    }

    @Override
    public String toString() {
        return "No{" +
                "data='" + data + '\'' +
                ", nextNo=" + nextNo +
                '}';
    }
}

public class Main {
    public static void main(String[] args) {
        No<String> no1 = new No("Conteúdo no1");
        No<String> no2 = new No("Conteúdo no2");
        no1.setNextNo(no2);
        No<String> no3 = new No("Conteúdo no3");
        no2.setNextNo(no3);
        No<String> no4 = new No("Conteúdo no4");
        no3.setNextNo(no4);

        // no1 -> no2 -> no3 -> no4 -> null

        System.out.println("------------------");
        System.out.println(no1);
        System.out.println(no1.getNextNo());
        System.out.println(no1.getNextNo().getNextNo());
        System.out.println(no1.getNextNo().getNextNo().getNextNo());
        System.out.println(no1.getNextNo().getNextNo().getNextNo().getNextNo());
    }
}
```

# Pilhas

- LIFO: last In, First Out
- O último elemento que entra é o primeiro a sair
- O nó que está na base (primeiro nó) sempre apontará para `null`
- O metódo `top` pegará a informação do último nó adicionado (no topo)
- O metódo `push` adiciona um nova nó ao topo
- O metódo `pop`remove o último nó (do topo) e o retorna

## Implementando os metodos

- Classe Nó

```Java
public class No {
    private int dado;
    private No refNo = null;

    No() {}

    No(int dado) {
        this.dado = dado;
    }

    public int getDado() {
        return dado;
    }

    public void setDado(int dado) {
        this.dado = dado;
    }

    public No getRefNo() {
        return refNo;
    }

    public void setRefNo(No refNo) {
        this.refNo = refNo;
    }

    @Override
    public String toString() {
        return "No{" +
                "dado=" + dado +
                '}';
    }
}
```

- Classe Pilha

```Java
public class Pilha {

    private No refNoEntradaPilha;

    Pilha() {
        this.refNoEntradaPilha = null;
    }

    public No top() {
        return refNoEntradaPilha;
    }

    public void push(No novoNo) {
        No refAuxiliar = refNoEntradaPilha;
        this.refNoEntradaPilha = novoNo;
        refNoEntradaPilha.setRefNo(refAuxiliar);
    }

    public No pop() {
        if (this.isEmpty()) return null;
        No removedNo = this.refNoEntradaPilha;
        this.refNoEntradaPilha = this.refNoEntradaPilha.getRefNo();
        return removedNo;
    }

    public boolean isEmpty() {
        return refNoEntradaPilha == null;
    }

    @Override
    public String toString() {
        String strR = "---------------\n";
        strR += "       pilha\n";
        strR += "-----------------\n";
        No noAuxiliar = this.refNoEntradaPilha;
        while (noAuxiliar != null) {
            strR += "[Nó{dado= " + noAuxiliar + "}]\n";
            noAuxiliar = noAuxiliar.getRefNo();
        }
        strR += "=================";
        return strR;
    }
}

```

- Classe Main

```Java
public class Main {
    public static void main(String[] args) {
        Pilha pilha = new Pilha();

        pilha.push(new No(1));
        pilha.push(new No(2));
        pilha.push(new No(3));
        pilha.push(new No(4));
        pilha.push(new No(5));

        System.out.println(pilha);
    }
}
```
