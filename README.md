class Banco:
    def __init__(self, nome):
        self.nome = nome
        self.clientes = []
        self.contas = []

    def adicionar_cliente(self, cliente):
        self.clientes.append(cliente)

    def adicionar_conta(self, conta):
        self.contas.append(conta)

    def mostrar_clientes(self):
        for cliente in self.clientes:
            print(f"Cliente: {cliente.nome}, CPF: {cliente.cpf}")

    def mostrar_contas(self):
        for conta in self.contas:
            print(f"Conta {conta.numero}, Saldo: {conta.saldo}, Cliente: {conta.cliente.nome}")


class Cliente:
    def __init__(self, nome, cpf):
        self.nome = nome
        self.cpf = cpf


class Conta:
    def __init__(self, numero, cliente, saldo_inicial=0):
        self.numero = numero
        self.cliente = cliente
        self.saldo = saldo_inicial

    def depositar(self, valor):
        self.saldo += valor
        print(f"Depositado: {valor}, Novo saldo: {self.saldo}")

    def sacar(self, valor):
        if self.saldo >= valor:
            self.saldo -= valor
            print(f"Sacado: {valor}, Novo saldo: {self.saldo}")
        else:
            print("Saldo insuficiente")

    def mostrar_saldo(self):
        print(f"Saldo atual: {self.saldo}")


class ContaCorrente(Conta):
    def __init__(self, numero, cliente, saldo_inicial=0, limite=0):
        super().__init__(numero, cliente, saldo_inicial)
        self.limite = limite

    def sacar(self, valor):
        if self.saldo + self.limite >= valor:
            self.saldo -= valor
            print(f"Sacado: {valor}, Novo saldo: {self.saldo}")
        else:
            print("Saldo insuficiente, incluindo o limite")


class ContaPoupanca(Conta):
    def __init__(self, numero, cliente, saldo_inicial=0, rendimento=0.01):
        super().__init__(numero, cliente, saldo_inicial)
        self.rendimento = rendimento

    def aplicar_rendimento(self):
        self.saldo += self.saldo * self.rendimento
        print(f"Rendimento aplicado: {self.saldo * self.rendimento}, Novo saldo: {self.saldo}")


banco = Banco("Meu Banco")

cliente1 = Cliente("Alice", "123.456.789-00")
cliente2 = Cliente("Bob", "987.654.321-00")

conta1 = ContaCorrente("001", cliente1, saldo_inicial=1000, limite=500)
conta2 = ContaPoupanca("002", cliente2, saldo_inicial=5000, rendimento=0.02)

banco.adicionar_cliente(cliente1)
banco.adicionar_cliente(cliente2)
banco.adicionar_conta(conta1)
banco.adicionar_conta(conta2)

banco.mostrar_clientes()
banco.mostrar_contas()

conta1.depositar(200)
conta1.sacar(1500)
conta2.aplicar_rendimento()
