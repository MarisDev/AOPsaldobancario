public abstract class Conta {
    private String tipoConta;
    private String tipoCliente;
    private double saldo;

    public Conta(String tipoConta, String tipoCliente, double saldoInicial) {
        this.tipoConta = tipoConta;
        this.tipoCliente = tipoCliente;
        this.saldo = saldoInicial;
    }

    public double getSaldo() {
        return saldo;
    }

    public void depositar(double valor) {
        saldo += valor;
        System.out.println("Depósito realizado. Novo saldo: " + saldo);
    }

    public void sacar(double valor) {
        saldo -= valor;
        System.out.println("Saque realizado. Novo saldo: " + saldo);
    }

    @Override
    public String toString() {
        return "Conta{" +
                "tipoConta='" + tipoConta + '\'' +
                ", tipoCliente='" + tipoCliente + '\'' +
                ", saldo=" + saldo +
                '}';
    }
}

public class ContaPoupanca extends Conta {
    public ContaPoupanca(String tipoCliente, double saldoInicial) {
        super("Poupança", tipoCliente, saldoInicial);
    }
}

public class ContaInvestimento extends Conta {
    public ContaInvestimento(String tipoCliente, double saldoInicial) {
        super("Investimento", tipoCliente, saldoInicial);
    }
}

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Pointcut;

@Aspect
public class VerificacaoSaldoAspect {

    // Define um ponto de corte para todos os métodos "sacar" em classes que estendem Conta
    @Pointcut("execution(void Conta.sacar(double)) && target(conta) && args(valor)")
    public void verificarSaldo(Conta conta, double valor) {}

    // Antes da execução do método "sacar", verifica o saldo
    @Before("verificarSaldo(conta, valor)")
    public void beforeSaque(Conta conta, double valor) {
        if (conta.getSaldo() < valor) {
            throw new IllegalArgumentException("Saldo insuficiente para realizar o saque.");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        try {
            Conta poupanca = new ContaPoupanca("Cliente Individual", 1000);
            Conta investimento = new ContaInvestimento("Cliente Empresarial", 500);

            System.out.println(poupanca);
            poupanca.sacar(200); // Saque válido
            System.out.println(poupanca);

            System.out.println(investimento);
            investimento.sacar(600); // Vai lançar exceção
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }
}
