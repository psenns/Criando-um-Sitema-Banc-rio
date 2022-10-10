# Criando-um-Sitema-Banc-rio
Primeiro projeto Criando um sistema bancário com Python em dio.me

menu = """
    [d] Depositar
    [s] Sacar
    [t] Transferência
    [p] Aplicação
    [cp] Calculadora de Aplicação
    [e] Extrato
    [x] Sair
    
 =>"""

saldo = 0
limite = 500
limite_pix = 1000
extrato = ""
quantidade_saque = 0
limite_saque = 3

while True:

    opcao = input(menu)

    if opcao == "d":
        valor = float(input("Digite o valor que deseja depositar: "))

        if valor > 0:
            saldo += valor
            extrato += f"Deposito de R$ {valor:.2f}\n"

        else:
            print("Não conseguimos realizar seu depósito. O valor digitado está incorreto!")


    elif opcao == "s":
        valor = float(input("Informe o valor que deseja sacar: "))

        excedeu_saldo = valor > saldo

        excedeu_limte = valor > limite

        excedeu_saques = quantidade_saque > limite_saque

        if excedeu_saldo:
            print("Saldo insuficiente! Deposite um valor para continuar transação.")

        elif excedeu_limte:
            print("Limite excedido! Aumente seu limite no caixa eletrônico ou diretamente com um consultor.")

        elif excedeu_saques:
            print("Você excedo o limite de Saque Diário. Tente novamente amanhã!")

        elif valor > 0:
            saldo -= valor
            extrato += f"Saque: R$ {valor:.2f}\n"
            quantidade_saque += 1

        else:
            print("Opção inválida! Tente novamente.")

    elif opcao == "t":
        transf_agencia = int(input("Digite o número da agência: "))

        transf_conta = int(input("Digite o número da conta: "))

        transf_valor = float(input("Quanto você deseja transferir: "))

        excedeu_saldo_transf = transf_valor > saldo

        excedeu_limite_trans = transf_valor > limite

        if excedeu_saldo_transf:
            print("Saldo insuficiente para realizar transferência!")

        elif excedeu_limite_trans:
            print("Limite excedido! Aumente seu limite no caixa eletrônico ou diretamente com um consultor.")

        elif transf_valor > 0:
            saldo -= transf_valor
            extrato += f"Transferência: R$ {transf_valor:.2f}\n"

        else:
            print("Opção inválida! Tente novamente.")

    elif opcao == "p":
        print(
            "Seja bem vindo a aplicação do Banco Psenns! Aqui você aplica seu juros com juros de 2% a.m. Aqui seu dinheiro rende!")
        valor_aplicado = float(input("Digite o valor que você deseja aplicar: "))

        aplicado_excedeu_saldo = valor_aplicado > saldo

        if aplicado_excedeu_saldo:
            print("Saldo insuficiente para realizar aplicação!")

        elif valor_aplicado > 0:
            saldo -= valor_aplicado
            extrato += f"Valor aplicado: R$ {valor_aplicado:.2f}"
        else:
            print("Opção inválida! Tente novamente.")
    elif opcao == "cp":
        aplicado_valor = float(input("Quanto você deseja aplicar: "))
        meses = int(input("Digite por quantos meses deseja aplicar: "))
        calculo_aplicado = (aplicado_valor*2/100)*meses

        if aplicado_valor > 0:
            print(f"A aplicação rendeu: R$ {calculo_aplicado:.2f}")
            print(f"O novo saldo da sua conta será de R$ {aplicado_valor + calculo_aplicado:.2f} ao final de {meses} meses.")
        else:
            print("Opção inválida! Tente novamente.")


    elif opcao == "e":
        print("\nºººººººººººº EXTRATO ºººººººººººº")
        print("Não houve saques até o momento." if not extrato else extrato)
        print(f"\nSaldo: R$ {saldo:.2f}")
        print("ºººººººººººººººººººººººººººººººººººº")

    elif opcao == "x":
        print('Até breve!')
        break

    else:
        print("Operaçao inválida! Tente novamente.")
