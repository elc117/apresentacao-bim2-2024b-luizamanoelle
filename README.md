# **Entendendo `super` em Java**

## **O que é `super` em Java?**

Em Java, `super` é uma palavra-chave usada para fazer referência à **superclasse** (classe pai) a partir de uma **subclasse** (classe filha). É especialmente útil ao trabalhar com **herança**, permitindo acessar membros (atributos e métodos) ou invocar o construtor da classe pai.

---

## **Para que serve `super`?**

1. **Chamar o construtor da classe pai**: Utilizamos `super()` para invocar um construtor específico da superclasse.
2. **Acessar membros da superclasse**: Usamos `super.` para acessar métodos ou atributos da superclasse, mesmo quando sobrescritos na subclasse.

---

## **Exemplos Práticos**

### **1. Acessando o construtor da classe pai com `super()`**

Vamos considerar uma superclasse `Veiculo`:

```java
public class Veiculo {
    private String nome;
    private int tipo;

    // Construtor
    public Veiculo(String nome, int tipo) {
        this.nome = nome;
        this.tipo = tipo;
    }
}

```

Agora, criamos a subclasse `Aviao`, que herda de `Veiculo`:

```java
public class Aviao extends Veiculo {
    private int categoria;

    // Construtor
    public Aviao(String nome, int categoria) {
        // Chamando o construtor da superclasse
        super(nome, 10); // 10 como exemplo para 'tipo'
        this.categoria = categoria;
    }
}

```

Aqui, `super(nome, 10)` chama o construtor da classe pai para inicializar `nome` e `tipo`.

---

### **2. Utilizando `super.` para acessar métodos ou atributos da superclasse**

Se a superclasse possui métodos que você deseja usar ou complementar, você pode acessá-los com `super.`.

Atualizamos a classe `Veiculo` para incluir um método `info`:

```java
public class Veiculo {
    private String nome;
    private int tipo;

    public Veiculo(String nome, int tipo) {
        this.nome = nome;
        this.tipo = tipo;
    }

    public void info() {
        System.out.printf("Nome: %s%n", this.nome);
        System.out.printf("Tipo: %d%n", this.tipo);
    }
}

```

Na classe `Aviao`, sobrescrevemos o método `info` para incluir a categoria:

```java
public class Aviao extends Veiculo {
    private int categoria;

    public Aviao(String nome, int categoria) {
        super(nome, 10);
        this.categoria = categoria;
    }

    @Override
    public void info() {
        // Chamando o método info da superclasse
        super.info();
        System.out.printf("Categoria: %d%n", this.categoria);
    }
}

```

**Saída do programa**:

```java
public class Main {
    public static void main(String[] args) {
        Aviao v1 = new Aviao("Voa", 1);
        v1.info();
    }
}

```

```
Nome: Voa
Tipo: 10
Categoria: 1

```

---

### **3. Por que usar `super()` no construtor da subclasse?**

Se a superclasse tiver um construtor que exige parâmetros, o Java **não gerará automaticamente** um construtor padrão. Nesse caso, você **deve** usar `super()` na subclasse para garantir que o construtor correto da superclasse seja chamado.

Exemplo: Sem `super()`, o seguinte código gera um erro de compilação:

```java
public class Aviao extends Veiculo {
    private int categoria;

    public Aviao(String nome, int categoria) {
        // ERRO: Superclasse não possui um construtor sem parâmetros
        this.categoria = categoria;
    }
}

```

**Solução: Utilize `super()` com os parâmetros exigidos**:

```java
public Aviao(String nome, int categoria) {
    super(nome, 10);
    this.categoria = categoria;
}

```

---

### **4. Quando sobrescrever métodos e utilizar `super.`?**

Se você sobrescrever um método da superclasse, ainda pode acessá-lo usando `super.` dentro do método sobrescrito. Isso é útil para complementar a funcionalidade do método pai.

Exemplo:

```java
@Override
public void info() {
    super.info(); // Chama o método da superclasse
    System.out.printf("Categoria: %d%n", this.categoria); // Adiciona funcionalidade
}

```

---

## **Dicas Práticas**

1. **Quando usar `super()`?**
    - Use `super()` no **primeiro comando** do construtor da subclasse para inicializar os atributos definidos na superclasse.
2. **Quando usar `super.`?**
    - Use `super.` para acessar membros da superclasse que estão ocultos ou sobrescritos pela subclasse.
3. **Regras importantes:**
    - Se você **não chamar `super()`**, o Java tentará invocar o construtor padrão da superclasse automaticamente. Caso a superclasse não tenha um construtor sem parâmetros, um erro de compilação será gerado.
    - Sempre utilize `super()` como a primeira linha do construtor da subclasse.

---

## Referências

https://www.youtube.com/watch?v=8VzFrNPkN6U

https://www.datacamp.com/pt/doc/java/super

:)
