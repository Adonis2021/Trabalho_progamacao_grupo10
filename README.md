# Trabalho_progamacao_grupo10
SNACK_BAR

import java.util.List;
import java.util.Scanner;
import java.util.ArrayList;


class ItemVenda {
    private String nome;
    private double preco;
    private String dataValidade;
    private double quantidade;

    public ItemVenda(String nome, double preco, String dataValidade, double quantidade) {
        this.nome = nome;
        this.preco = preco;
        this.dataValidade = dataValidade;
        this.quantidade = quantidade;
    }

    // getters e setters

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public double getPreco() {
        return preco;
    }

    public void setPreco(double preco) {
        this.preco = preco;
    }

    public String getDataValidade() {
        return dataValidade;
    }

    public void setDataValidade(String dataValidade) {
        this.dataValidade = dataValidade;
    }

    public double getQuantidade() {
        return quantidade;
    }

    public void setQuantidade(double quantidade) {
        this.quantidade = quantidade;
    }
}

class Pedido {
    private String nomeCliente;
    private List<ItemVenda> itensConsumidos;
    private double taxaServico;
    private int quantidade;


    public Pedido(String nomeCliente, List<ItemVenda> itensConsumidos, double taxaServico) {
        this.nomeCliente = nomeCliente;
        this.itensConsumidos = itensConsumidos;
        this.taxaServico = taxaServico;
        this.quantidade = quantidade;
    }

    // getters e setters

    public String getNomeCliente() {
        return nomeCliente;
    }

    public void setNomeCliente(String nomeCliente) {
        this.nomeCliente = nomeCliente;
    }

    public List<ItemVenda> getItensConsumidos() {
        return itensConsumidos;
    }

    public void setItensConsumidos(List<ItemVenda> itensConsumidos) {
        this.itensConsumidos = itensConsumidos;
    }

    public double getTaxaServico() {
        return taxaServico;
    }

    public void setTaxaServico(double taxaServico) {
        this.taxaServico = taxaServico;
    }

    public double calcularTotal() {
        double total = 0.0;
        for (ItemVenda item : itensConsumidos) {
            total += item.getPreco();
        }
        total += taxaServico;
        return total;
    }
}

class FaturaRecibo {
    private final Pedido pedido;

    public FaturaRecibo(Pedido pedido) {
        this.pedido = pedido;
    }

    public void gerarFaturaRecibo() {
        System.out.println("======== Fatura/Recibo ========");
        System.out.println("Cliente: " + pedido.getNomeCliente());
        System.out.println("Itens Consumidos:");
        for (ItemVenda item : pedido.getItensConsumidos()) {
            System.out.println("- " + item.getNome() + " - AKZ " + item.getPreco());
        }
        System.out.println("Taxa de Servico: AKZ " + pedido.getTaxaServico());
        System.out.println("Total: AKZ " + pedido.calcularTotal());
        System.out.println("===============================");
    }
}

class SnackBar {
    public static void main(String[] args) {
        try (Scanner scanner = new Scanner(System.in)) {
            List<ItemVenda> itensMenu = new ArrayList<>();
            
            // Adicionar itens de venda ao menu
            itensMenu.add(new ItemVenda("Pizza Margherita", 7000, "10/06/2023", 500.0));itensMenu.add(new ItemVenda("Pizza de atum", 7000, "10/06/2023", 500.0));itensMenu.add(new ItemVenda("Pizza 4 Estacoes", 7500, "10/06/2023", 500.0));itensMenu.add(new ItemVenda("Pizza de carne", 7000, "10/06/2023", 500.0));
            itensMenu.add(new ItemVenda("Lanches", 500, "12/06/2023", 300.0));
            itensMenu.add(new ItemVenda("Salgadinho de Queijo", 100, "15/06/2023", 100.0));
            
         itensMenu.add(new ItemVenda("Salgadinho de carne", 100, "15/06/2023", 100.0)); itensMenu.add(new ItemVenda("Salgadinho de Atum", 100, "15/06/2023", 100.0)); itensMenu.add(new ItemVenda("Salgadinho de Queijo", 100, "15/06/2023", 100.0));
            
            System.out.println("==== Cardapio ====");
            for (int i = 0; i < itensMenu.size(); i++) {
                ItemVenda item = itensMenu.get(i);
                System.out.println((i + 1) + ". " + item.getNome() + " - AKZ " + item.getPreco());
            }
            System.out.println("=================");
            
            System.out.print("Digite o numero do item que deseja : ");
            int opcao = scanner.nextInt();
            ItemVenda itemSelecionado = itensMenu.get(opcao - 1);
            
            System.out.print("Digite o nome do cliente: ");
            scanner.nextLine(); // Consumir a quebra de linha pendente
            String nomeCliente = scanner.nextLine();
            
            System.out.print("Digite a taxa de servico: ");
            double taxaServico = scanner.nextDouble();
            
            List<ItemVenda> itensConsumidos = new ArrayList<>();
            itensConsumidos.add(itemSelecionado);
            
            Pedido pedido = new Pedido(nomeCliente, itensConsumidos, taxaServico);
            FaturaRecibo faturaRecibo = new FaturaRecibo(pedido);
            faturaRecibo.gerarFaturaRecibo();
            
            System.out.print("Digite o valor recebido : ");
            double valorRecebido = scanner.nextDouble();
            
            double troco = valorRecebido - pedido.calcularTotal();
            System.out.println("Troco: AKZ " + troco);
        }
    }
}
